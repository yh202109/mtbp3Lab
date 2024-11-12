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
See table-kappa3-1_.

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
Bias, Prevalence and Adjusted Kappas
*************

All discussion in this section are based on Byrt, T., Bishop, J., & Carlin, J. B. (1993) [1]_ [2]_ [3]_.

Bias Index (BI) 
=============

For two raters and two categories (:math:`J=2`), Byrt et al. define Bias Index (BI) as difference of probability of one rating from two raters, which can be estimated as:

.. math::
  \hat{BI} = \frac{1}{n}(N_{1 \bullet} - N_{\bullet 1}) = \frac{1}{n}(N_{12} - N_{21}).

:math:`\hat{BI}` has the following properties:

- when two off-diagonal counts are equal, which means :math:`N_{12} = N_{21}`, then :math:`\hat{BI} = 0`;
- when two raters have the same frequencies of ratings, which means :math:`N_{1 \bullet} = N_{\bullet 1}`, and  :math:`N_{11}+N_{12} = N_{11}+N_{21}`, then :math:`\hat{BI} = 0`; 
- when :math:`N_{12} = n` or :math:`N_{21}=n`, :math:`|\hat{BI}|=1`.


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

See table-1_.

.. list-table:: Counts for 2 categories
   :widths: 10 10 10 10
   :header-rows: 1
   :name: table-1

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

See illustration in table-2_.

.. list-table:: Counts for 2 categories
   :widths: 10 10 10 10
   :header-rows: 1
   :name: table-2

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

Based on table-2_, we can find adjusted :math:`p_E^{(BAPA)}` and :math:`p_O^{(BAPA)}`:

.. math::
  p_E^{(BAPA)} = \frac{1}{n^2} \left( \frac{n}{2}\frac{n}{2} + \frac{n}{2}\frac{n}{2} \right) = \frac{1}{2},

and 

.. math::
  p_O^{(BAPA)} = \frac{1}{n} \left( N_{11}^{(PA)} + N_{22}^{(PA)} \right) = \frac{1}{n} \left( N_{11} + N_{22} \right) = p_O.


Therefore, the :math:`\kappa` value based on table-2_ can be calculated as:

.. math::
  \kappa^{(BAPA)} = \frac{p_O - 0.5}{1 - 0.5} = 2p_O - 1,

which is a linear function of :math:`p_O` with possible values between -1 and 1.

*************
Reference
*************

.. [1] Byrt, T., Bishop, J., & Carlin, J. B. (1993). Bias, prevalence and kappa. Journal of clinical epidemiology, 46(5), 423–429. https://doi.org/10.1016/0895-4356(93)90018-v
.. [2] SAS. (year). The SURVEYFREQ Procedure: Kappa Coefficients. https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.4/statug/statug_surveyfreq_details57.htm
.. [3] SAS. (year). The FREQ Procedure: Tests and Measures of Agreement. https://documentation.sas.com/doc/en/statug/15.2/statug_freq_details78.htm
