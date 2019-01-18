NTU-ML-Foundations-BY-Hsuan-Tien-Lin(Homework1)
===
总述
---
  本文件中包含了台湾大学林轩田《机器学习基石》的coursera平台上的配套练习中的课后作业，本部分为作业1中的编程作业部分，使用C++实现，本代码参考了CSDN博主Mac Jiang的部分代码，并在原代码的基础上进行了部分修改，并在注释中附加了对代码的个人理解和补充。<br>
<br>
  作业1中主要涉及的算法为机器学习中的一种比较简单的分类算法：自动感知机（PLA）及其演进算法pocket算法，作业要求是编写PLA算法和pocket算法在所给的数据集上实现数据的分类。<br>
<br>
## PLA算法<br>
  PLA算法实现数据分类所遵循的策略是“逐步修正”的方法，以二维平面上的数据二分问题为例，其所采用的方法是：首先在平面上随意取一条直线，看看哪些点分类错误，然后根据一定的遍历规则对平面上的所有点进行遍历，在遍历的过程中一旦发现有分类错误的点便进行修正，即修正直线的位置，使这个错误的点变成分类正确的点。接下来继续进行数据点的遍历，再对第二个、第三个错误点进行修正，并在此过程中不断修正直线的位置，使这些错误点变成正确的点，知道所有的点都完全分类正确了，就得到了最好的分类线（或者是分类面、超平面等），这种“逐步修正的”策略便是PLA的核心思想。<br>
  * 算法实现<br>
    由于该算法是实现线型分类功能的算法，所以该算法要求数据集为线型可分的数据集，算法返回的结果也是由一组权重表示的直线、平面或者超平面，该算法实现的伪代码如下：<br>
    for t = 0,1,2...<br>
      1、遍历数据点，计算每个数据点xn(t)在第t轮迭代中的权重Wt下的计算结果Wt*xn(t)，并与该点对应的标签值yn进行比较，进行判断计算：<br>
      sign(Wt*xn(t))==yn<br>
      2、如果1中的判断结果为false，这对权重进行修正，修正公式为：<br>
      Wt+1 = Wt + yn*xn(t)<br>
      3、继续进行t轮迭代，直到没有错误分类点<br>
    return Wpla<br>
 ## pocket算法<br>
  pocket算法是PLA算法的演进算法，这种算法放宽了对分类结果的要求，允许分类不正确的点出现，即允许返回结果中出现噪声。pocket算法的算法流程和PLA算法的流程类似，首先初始化权重W0，计算出在这个初始化的分类面中，分类错误的点的个数，然后对错误点进行修正，更新W，得到一组新的权重，然后再计算其对应的分类错误点的个数，并与之前的错误点的个数进行比较，取个数较小的分类面作为当前选择的分类面，之后继续进行迭代，不断比较当前分类错误的点的个数与上一次分类错误的点的个数，并选择个数最小的那一组参数进行保存，直到迭代次数完成后，选取分类错误数最小的那一组参数作为最后的返回结果Wpocket。<br>
    * 算法实现<br>
    for t = 0,1,2...N<br>
      1、遍历数据点，并随机找到一组在Wt的权重下分类错误的点xn(t)<br>
      2、更新权值：Wt+1 = Wt + yn*xn(t)<br>
      3、比较Wt+1和Wt的性能，如果Wt+1下的分类错误点的个数比Wt下的分类错误点的个数少的话，则保留当前权值Wt+1，否则不更新。<br>
      4、继续迭代，直到达到设定迭代次数<br>
    return Wpla<br>
  
##Q15
---

其中，Q15和Q16是使用自动感知机PLA算法对所给的数据集进行二分类，Q18为使用pocket算法对数据集进行二分类。
