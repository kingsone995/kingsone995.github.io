## 概述
本文简要说明在MAC下如何使用latex

### 1.基本环境
MacTex + Sublime + Skim

### 1.使用参考文献
1. 通过EndNote收集文献；
2. 将收集到的文献，通过“文件”-“导出”，输出样式中选择"BibTex Export",生成的其中一个文献如下：
```
@article{RN1780,
   author = {Li, Kai and Wang, Qiang and Wu, Jia and Yu, Haiyang and Zhang, Dongsheng},
   title = {Calibration error for dual-camera digital image correlation at microscale},
   journal = {Optics and Lasers in Engineering},
   volume = {50},
   number = {7},
   pages = {971-975},
   ISSN = {0143-8166},
   DOI = {10.1016/j.optlaseng.2012.01.025},
   url = {http://www.sciencedirect.com/science/article/pii/S0143816612000395},
   year = {2012},
   type = {Journal Article}
}
```
3. 将刚刚生成的文本文件直接改名为MyBib.bib，并拷贝到tex文件所在目录。
4. 在tex文件的\end{document}之前，加上两句,加完后的结果如下：
```
\bibliographystyle{plain}
\bibliography{MyBib}
\end{document}
```
其中MyBib就是我们刚刚生成的参考文献清单。
plain就是参考文献的输出格式（毕业论文格式检查中，很多就是参考文献格式问题）。
5. 参考文献引用如下,其中RN1780就是文献ID，输入cite和{}后，一般会自动跳出来。
```
\cite{RN1780}
```
6. 编译两次，就能生成对应的参考文献格式。

引用地方原文：
```
从上一章我们知道，N个点的DTF需要做很多次运算。我们先来看一看，一个正向DFT需要做几次计算\cite{RN1780,RN1087,RN1778,RN1779}。\\
```
引用地方效果：
```
从上一章我们知道，N 个点的 DTF 需要做很多次运算。我们先来看一看，一个正向 DFT 需要做几次计算 [1–4]。
```
参考文献输出格式：
```
[1] Ikhyun Lee, Muhammad Tariq Mahmood, and Tae-Sun Choi. Adaptive window selection for 3d shape recovery from image focus. Optics and Laser Technology, 45(1):21–31, 2013.
[2] Kai Li, Qiang Wang, Jia Wu, Haiyang Yu, and Dongsheng Zhang. Calibration error for dual-camera digital image correlation at microscale. Optics and Lasers in Engineering, 50(7):971–975, 2012.
[3] K. B. Lim, W. L. Kee, and D. L. Wang. Virtual camera calibration and stereo correspondence of single-lens bi-prism stereovision system using geometrical approach. Signal Processing-Image Communication, 28(9):1059–1071, 2013.
[4] Said Pertuz, Domenec Puig, and Miguel Angel Garcia. Analysis of focus measure operators for shape-from-focus. Pattern Recognition, 46(5):1415–1432, 2013.
```