..
    #  Copyright (C) 2023-2024 Y Hsu <yh202109@gmail.com>
    #
    #  This program is free software: you can redistribute it and/or modify
    #  it under the terms of the GNU General Public license as published by
    #  the Free software Foundation, either version 3 of the License, or
    #  any later version.
    #
    #  This program is distributed in the hope that it will be useful,
    #  but WITHOUT ANY WARRANTY; without even the implied warranty of
    #  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
    #  GNU General Public License for more details
    #
    #  You should have received a copy of the GNU General Public license
    #  along with this program. If not, see <https://www.gnu.org/license/>
   

.. role:: red-b

.. role:: red

.. role:: bg-ltsteelblue

#############
Reliability/cate/Kappa Variations
#############

:red-b:`Disclaimer:`
:red:`This page is provided only for studying and practicing. The author does not intend to promote or advocate any particular analysis method or software.`

*************
Background
*************

Cohen's kappa (:math:`\kappa`) is a statistic used for describing inter-rater reliability of two raters (or intra-rater) with categorical rating outcomes [1]_. 
This page discusses some variations.

*************
Notation 
*************

For two raters and two or more category ratings, let :math:`Y_{r,i} \in \{v_1,\ldots, v_J \}` represent the rating 
from rater :math:`r \in \{1,2\}` for sample :math:`i \in \{ 1, \ldots, n \}`.
Let :math:`N_{j_1,j_2}` represent the total number of samples that received ratings :math:`(v_{j_1}, v_{j_2})` from two raters, where :math:`j_1,j_2 \in \{1,\ldots,J\}`.
See :numref:`table-kappa3-1`.

.. _table-kappa3-1:

.. list-table:: Counts for 3 or more categories
   :widths: 10 10 10 10 10 10
   :header-rows: 1

   * - 
     - Rater 2: :math:`v_1`
     - Rater 2: :math:`v_2`
     - Rater 2: :math:`v_3`
     - :math:`\ldots` 
     - Row Total
   * - **Rater 1:** :math:`v_1`
     - :math:`N_{11}`
     - :math:`N_{12}` 
     - :math:`N_{13}` 
     - :math:`\ldots` 
     - :math:`N_{1\bullet}` 
   * - **Rater 1:** :math:`v_2`
     - :math:`N_{21}`
     - :math:`N_{22}` 
     - :math:`N_{23}` 
     - :math:`\ldots` 
     - :math:`N_{2\bullet}` 
   * - **Rater 1:** :math:`v_3`
     - :math:`N_{31}`
     - :math:`N_{32}` 
     - :math:`N_{33}` 
     - :math:`\ldots` 
     - :math:`N_{3\bullet}` 
   * - :math:`\vdots` 
     - :math:`\vdots`
     - :math:`\vdots`
     - :math:`\vdots`
     - :math:`\ddots` 
     - :math:`\vdots` 
   * - **Column Total**
     - :math:`N_{\bullet 1}`
     - :math:`N_{\bullet 2}` 
     - :math:`N_{\bullet 3}` 
     - :math:`\ldots` 
     - :math:`n` 

The observed raw percentage of agreement is defined as :math:`p_O = \sum_{j=1}^J N_{jj} / n`.
The expected number of agreement is estimated by
:math:`\sum_{j=1}^J\hat{E}_{j} = \frac{1}{n}\sum_{j=1}^J N_{\bullet j} N_{j\bullet} \equiv n p_E`.
The Cohen's :math:`\kappa` statistic is calculated as :math:`\kappa = \frac{p_O - p_E}{1-p_E}`.
The SE of :math:`\kappa` is calculated as :math:`\sqrt{\frac{p_O(1-p_O)}{n(1-p_E)^2}}`.

*************
Bias, Prevalence and Adjusted Kappas (Byrt et al., 1993)
*************

All discussion in this section are based on Byrt, T., Bishop, J., & Carlin, J. B. (1993) [1]_ unless cited otherwise.

Bias Index (BI) 
=============

For two raters and two categories (:math:`J=2`), Byrt et al. define Bias Index (BI) as difference of probability of one rating from two raters, which can be estimated as:

.. math::
  \hat{BI} = \frac{1}{n}(N_{1 \bullet} - N_{\bullet 1}) = \frac{1}{n}(N_{12} - N_{21}).

:math:`\hat{BI}` has the following properties:

- when two off-diagonal counts are equal, which means :math:`N_{12} = N_{21}`, then :math:`\hat{BI} = 0`;
- when two raters have the same frequencies of ratings, which means :math:`N_{1 \bullet} = N_{\bullet 1}`, and  :math:`N_{11}+N_{12} = N_{11}+N_{21}`, then :math:`\hat{BI} = 0`; 
- when :math:`N_{12} = n` or :math:`N_{21}=n`, :math:`|\hat{BI}|=1`.

Note that the sign of :math:`\hat{BI}` depends on which rater (:math:`j=1` or :math:`j=2`) is assigned as "rater A".
Within this page, rater :math:`j=2` is corresponding to the rater labeled "A" in Byrt et al. (1993) to have similar table structures.

Bias-adjusted Kappa (BAK) 
=============

BAK is defined as kappa calculated by replacing :math:`N_{12}` and :math:`N_{21}` with 

.. math::
  N_{12}^{(BA)} = N_{21}^{(BA)} = \frac{1}{2}(N_{12} + N_{21}).

That yields

.. math::
  N_{1 \bullet}^{(BA)} = N_{\bullet 1}^{(BA)} = N_{11} + \frac{1}{2}(N_{12} + N_{21}),

and 

.. math::
  N_{2 \bullet}^{(BA)} = N_{\bullet 2}^{(BA)} = N_{22} + \frac{1}{2}(N_{12} + N_{21}).

See :numref:`table-kappa3-2`.

.. _table-kappa3-2:

.. list-table:: Adjusted counts for 2 categories adjusted - using BA
   :widths: 10 10 10 10
   :header-rows: 1

   * - 
     - Rater 2: :math:`v_1`
     - Rater 2: :math:`v_2`
     - Row Total
   * - **Rater 1:** :math:`v_1`
     - :math:`N_{11}`
     - :math:`N_{12}^{(BA)}` 
     - :math:`N_{1\bullet}^{(BA)}` 
   * - **Rater 1:**  :math:`v_2`
     - :math:`N_{12}^{(BA)}`
     - :math:`N_{22}` 
     - :math:`N_{2\bullet}^{(BA)}` 
   * - **Column Total**
     - :math:`N_{1 \bullet}^{(BA)}`
     - :math:`N_{2 \bullet}^{(BA)}` 
     - :math:`n`

Prevalence Index (PI)
=============

For two raters and two categories (:math:`J=2`), Byrt et al. defined Prevalence Index (PI) as the difference of averaged probability of two ratings, which can be estimated as:

.. math::
  \hat{PI} = \frac{1}{n}(N_{11} - N_{22}).

:math:`\hat{PI}` has the following properties:

- when :math:`N_{11} = N_{22}`, :math:`\hat{PI}=0`
- when :math:`N_{11} = n`, :math:`\hat{PI}=1`
- when :math:`N_{22} = n`, :math:`\hat{PI}=-1`

Prevalence-adjusted Bias-adjusted Kappa (PABAK)
=============

PABAK is defined as kappa calculated by replacing :math:`N_{12}` and :math:`N_{21}` as in BAK, and replacing :math:`N_{11}` and :math:`N_{22}` as:

.. math::
  N_{11}^{(PA)} = N_{22}^{(PA)} = \frac{1}{2}(N_{11} + N_{22}).

Note that a superscript "(PA)" is used to indicate there might be a difference between original observed :math:`N_{11}` and replaced :math:`N_{11}^{(PA)}`.

That yields

.. math::
  N_{1 \bullet}^{(BAPA)} = N_{\bullet 1}^{(BAPA)} = \frac{n}{2},

and 

.. math::
  N_{2 \bullet}^{(BAPA)} = N_{\bullet 2}^{(BAPA)} = \frac{n}{2}

See illustration in :numref:`table-kappa3-3`.

.. _table-kappa3-3:

.. list-table:: Adjusted counts for 2 categories adjusted - using both BA and PA
   :widths: 10 10 10 10
   :header-rows: 1

   * - 
     - Rater 2: :math:`v_1`
     - Rater 2: :math:`v_2`
     - Row Total
   * - **Rater 1:** :math:`v_1`
     - :math:`N_{11}^{(PA)}`
     - :math:`N_{12}^{(BA)}` 
     - :math:`\frac{n}{2}` 
   * - **Rater 1:**  :math:`v_2`
     - :math:`N_{12}^{(BA)}`
     - :math:`N_{11}^{(PA)}` 
     - :math:`\frac{n}{2}` 
   * - **Column Total**
     - :math:`\frac{n}{2}` 
     - :math:`\frac{n}{2}` 
     - :math:`n`

Based on :numref:`table-kappa3-3`, we can find adjusted :math:`p_E^{(BAPA)}` and :math:`p_O^{(BAPA)}`:

.. math::
  :label: eq_kappa3_pe

  p_E^{(BAPA)} = \frac{1}{n^2} \left( \frac{n}{2}\frac{n}{2} + \frac{n}{2}\frac{n}{2} \right) = \frac{1}{2},

and 

.. math::
  :label: eq_kappa3_po

  p_O^{(BAPA)} = \frac{1}{n} \left( N_{11}^{(PA)} + N_{22}^{(PA)} \right) = \frac{1}{n} \left( N_{11} + N_{22} \right) = p_O.


Therefore, the :math:`\kappa` value based on :numref:`table-kappa3-3` can be calculated as:

.. math::
  :label: eq_kappa3_1

  \kappa^{(BAPA)} = \frac{p_O - 0.5}{1 - 0.5} = 2p_O - 1,

which is a linear function of :math:`p_O` with possible values between -1 and 1.

Observed :math:`\kappa` as a function of PABAK, :math:`\hat{BI}`, and :math:`\hat{PI}`
=============

From :eq:`eq_kappa3_1`, we can see that [1]_ :sup:`(Equation 1 and Appendix A)` 

- :math:`p_O = \frac{1}{2}(\kappa^{(BAPA)} + 1)`
- combining :math:`p_O = \frac{1}{n}(N_{11}+N_{22})` and :math:`1-p_O = \frac{1}{n}(N_{12}+N_{21})`, the observed counts can be expressed as :numref:`table-kappa3-4` below

.. _table-kappa3-4:

.. list-table:: Observed counts for 2 categories - expressed using :math:`p_O`, :math:`BI` and :math:`PI`
   :widths: 10 10 10 10
   :header-rows: 1

   * - 
     - Rater 2: :math:`v_1`
     - Rater 2: :math:`v_2`
     - Row Total
   * - **Rater 1:** :math:`v_1`
     - :math:`\frac{n}{2}(p_O + \hat{PI})`
     - :math:`\frac{n}{2}(1 - p_O + \hat{BI})` 
     - :math:`\frac{n}{2}(1 + \hat{BI} + \hat{PI})` 
   * - **Rater 1:**  :math:`v_2`
     - :math:`\frac{n}{2}(1 - p_O - \hat{BI})`
     - :math:`\frac{n}{2}(p_O - \hat{PI})` 
     - :math:`\frac{n}{2}(1-\hat{BI}-\hat{PI})` 
   * - **Column Total**
     - :math:`\frac{n}{2}(1 - \hat{BI} + \hat{PI})`
     - :math:`\frac{n}{2}(1 + \hat{BI} - \hat{PI})` 
     - :math:`n`

From :numref:`table-kappa3-4`, we can see that :math:`p_E = \frac{1}{2}( 1 - \hat{BI}^2 + \hat{PI}^2)` and [1]_ :sup:`(Equation 1 and Appendix A)`

.. math::
  :label: eq_kappa3_2

  \kappa = \frac{\kappa^{(BAPA)}  + \hat{BI}^2 - \hat{PI}^2}{1 + \hat{BI}^2 - \hat{PI}^2}.


From :eq:`eq_kappa3_2`, we can observe change of :math:`\kappa` related to :math:`\kappa^{(BAPA)}`, :math:`\hat{BI}`, and :math:`\hat{PI}`.

Extend PABAK to More Than 2 Categories
=============

Bryt et al. (1993) [1]_ discuss :math:`PABAK` in details for ratings in 2 categories, 
and mentioned the equivalence of :math:`PABAK` to Bennett's :math:`S`, 
which can be calculated for more than 2 categories (:math:`J \geq 2`) and that yields variance used by SAS [2]_ [3]_.

For :math:`J \get 2`, :eq:`eq_kappa3_pe` and :eq:`eq_kappa3_po` become

.. math::
  :label: eq_kappa3_pe2

  p_E^{(BAPA)} = \frac{1}{n^2} \left( \sum_{j=1}^J \frac{n}{J}\frac{n}{J} \right) = \frac{1}{J},

and 

.. math::
  :label: eq_kappa3_po2

  p_O^{(BAPA)} = \frac{1}{n} \left( \sum_{j=1}^J N_{jj}^{(PA)} \right) = \frac{1}{n} \left( \sum_{j=1}^J N_{jj} \right) = p_O.


Combining :eq:`eq_kappa3_pe2` and :eq:`eq_kappa3_po2`, We can see that :eq:`eq_kappa3_1` becomes 

.. math::
  :label: eq_kappa3_3

  \kappa^{(BAPA)} = \frac{p_O - \frac{1}{J}}{1 - \frac{1}{J}},

which is a linear function of :math:`p_O` and a fixed value :math:`J`. The variance of :math:`\kappa^{(BAPA)}` in :eq:`eq_kappa3_3` can be expressed as 

.. math::
  :label: eq_kappa3_3var

  var\left(\kappa^{(BAPA)}\right) = \left(\frac{1}{1 - \frac{1}{J}}\right)^2\left(\frac{p_o(1-p_o)}{n}\right)
  = \left(\frac{J}{J - 1}\right)^2\left(\frac{p_o(1-p_o)}{n}\right)

We can see from :eq:`eq_kappa3_3var` the notation :math:`R = J = \frac{1}{p_E^{(BAPA)}}`.

Discussion from the Original Paper
=============

The first paragraph in the Discussion section of Bryt et al. (1993) [1]_ mentioned:

  "We have shown that for a :math:`2 \times 2` table of agreement kappa can be simply expressed in terms of three easily interpreted indices.
  ...
  The reexpression of kappa enables a clear explanation of the conceptually distinct and independent components that arise in the investigation of agreement."


Examples
=============

Example 1 
-------------

Given a fixed :math:`p_O`, the :math:`\kappa` statistic can be calculated as :math:`\kappa = 1 + \frac{p_O - 1}{1-p_E}`, which is a decreasing function of :math:`p_E`.
Byrt et al. (1993) [1]_ :sup:`(Table 1 and Table 2)` quoted an example from Feinstein and Cicchetti (1990), reproduced as :numref:`table_kappa3_ex1_1` and :numref:`table_kappa3_ex1_2`, showing that
given the same values of :math:`p_O`, different values of :math:`p_E` can yield :math:`\kappa` "more than 2-fold higher in one instance than the other".

.. _table_kappa3_ex1_1:

.. list-table:: :math:`p_O = 0.85` and Cohen's :math:`\kappa = 0.7`
   :widths: 10 10 10 10
   :header-rows: 1

   * - 
     - Rater 2: :math:`v_1`
     - Rater 2: :math:`v_2`
     - Row Total
   * - **Rater 1:** :math:`v_1`
     - 40
     - 9
     - 49
   * - **Rater 1:** :math:`v_2`
     - 6
     - 45
     - 51
   * - **Column Total**
     - 46
     - 54
     - 100

.. _table_kappa3_ex1_2:

.. list-table:: :math:`p_O = 0.85` and Cohen's :math:`\kappa = 0.32`
   :widths: 10 10 10 10
   :header-rows: 1

   * - 
     - Rater 2: :math:`v_1`
     - Rater 2: :math:`v_2`
     - Row Total
   * - **Rater 1:** :math:`v_1`
     - 80
     - 10
     - 90
   * - **Rater 1:** :math:`v_2`
     - 5
     - 5
     - 10
   * - **Column Total**
     - 85
     - 15
     - 100

*************
Reference
*************

.. [1] Byrt, T., Bishop, J., & Carlin, J. B. (1993). Bias, prevalence and kappa. Journal of clinical epidemiology, 46(5), 423–429. https://doi.org/10.1016/0895-4356(93)90018-v
.. [2] SAS. (year). The SURVEYFREQ Procedure: Kappa Coefficients. https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.4/statug/statug_surveyfreq_details57.htm
.. [3] SAS. (year). The FREQ Procedure: Tests and Measures of Agreement. https://documentation.sas.com/doc/en/statug/15.2/statug_freq_details78.htm
.. [4] Feinstein, A. R., & Cicchetti, D. V. (1990). High agreement but low kappa: I. The problems of two paradoxes. Journal of clinical epidemiology, 43(6), 543–549. https://doi.org/10.1016/0895-4356(90)90158-l
