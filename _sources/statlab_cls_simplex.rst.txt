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

#############
Classification/Multinomial and Simplex
#############

:red-b:`Disclaimer:`
:red:`This page is provided only for studying and practicing. The author does not intend to promote or advocate any particular analysis method or software.`

*************
Background
*************

For multi-class classification, the sum of probability of individual classes is restricted to one [1]_. 
This page includes discussions related to the space of probability values on a simplex.

*************
Notation 
*************

Let :math:`Y_{i}=c` be the class (group) of the :math:`i` th sample 
for :math:`i = 1, \ldots, n`, 
with class value :math:`c \in \{c_1,\ldots, c_K\}`, 
:math:`P(Y_i = c_k) = p_k`,
:math:`p_k \in [0,1]` for all :math:`k`,
and :math:`\sum_k p_k=1`.
Let :math:`N_k = \sum_{i=1}^n I(Y_i = c_k)`,
:math:`N = (N_1, \ldots, N_K)` with :math:`N_k \geq 0` and :math:`\sum_k N_k = n`.
The vector :math:`N` is a :math:`K` components compositional data point.
Let :math:`\hat{p} = (\hat{p}_1, \ldots, \hat{p}_K) \in [0,1]^K` with :math:`\sum_k \hat{p}_k = 1`.
The value space of :math:`\{\hat{p}\}` is a :math:`(K-1)`-dimensional standard (normalized) simplex [2]_.



*************
Example - Group-1
*************

.. list-table:: Spearman's :math:`\rho = 1.0`
   :widths: 10 10 10 
   :header-rows: 1
   :name: tbl_ex1

   * - 
     - :math:`Y_{i1}`
     - :math:`Y_{i2}`
   * - **Sample:** 1
     - 1
     - 4
   * - **Sample:** 2
     - 3
     - 6
   * - **Sample:** 3
     - 2
     - 5

.. list-table:: Spearman's :math:`\rho = -1.0`
   :widths: 10 10 10 
   :header-rows: 1
   :name: tbl_ex1

   * - 
     - :math:`Y_{i1}`
     - :math:`Y_{i2}`
   * - **Sample:** 1
     - 1
     - 6
   * - **Sample:** 2
     - 3
     - 4
   * - **Sample:** 3
     - 2
     - 5

*************
How-to 
*************

To use ``scipy.stats`` [3]_:

.. code:: python

  from scipy.stats import spearmanr

  y1 = [1, 3, 2]
  y2 = [4, 6, 5]

  rho, p_value = spearmanr(y1, y2)
  print("Spearman's rho:", rho)

*************
More Details
*************


*************
Reference
*************

.. [1] Djalil CHAFAÏ. (2013). Back to basics - Multinomial law. https://djalil.chafai.net/blog/2013/05/26/back-to-basics-multinomial-law/
.. [2] wiki. (year). Compositional data. https://en.wikipedia.org/wiki/Compositional_data
.. [3] John Aitchison. (1994). Principles of compositional data analysis. Institute of Mathematical Statistics Lecture Notes - Monograph Series Vol. 24, 73-81. https://doi.org/10.1214/lnms/1215463786 
.. [4] Michael Greenacre, Eric Grunsky, John Bacon-Shone, Ionas Erb, Thomas Quinn. (2023). Aitchison's Compositional Data Analysis 40 Years on: A Reappraisal. Statistical Science, Statist. Sci. 38(3), 386-410. https://projecteuclid.org/journals/statistical-science/volume-38/issue-3/Aitchisons-Compositional-Data-Analysis-40-Years-on-A-Reappraisal/10.1214/22-STS880.short

