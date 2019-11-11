# Quantum Computation and Quantum Information抄书笔记(1)

## 写在前面
最近深感自己学的东西都很不扎实，于是希望能把之前学过的和现在在学的整理一下，于是就有了这篇文章。

当然动机不只有这个。一方面，一直以来在互联网上受教良多，而中文互联网有价值的内容又是少之又少，现在希望能系统整理一下我熟悉的知识，穿插一些我的个人理解，为中文互联网写一些可能不那么垃圾的东西。另一方面，华罗庚曾讲“弄斧还要到班门”。把自己熟悉或自以为熟悉的东西写出来，放在能被人看到的地方，如果有幸被大佬看见，再被批判一番，想必是大有裨益的。

虽然主要是自娱自乐，不过还是希望被别人看见。知乎虽然有很多不好的地方，但它毕竟还是最好用、最开放的中文社区之一。大概只有写在这里才可能被搜索引擎爬到。

本文是Michael A.Nielsen和Isaac L.Chuang的*Quantum Computation and Quantum Information*(下称原书)的抄书笔记。本文不能替代读书学习。虽然我尽可能写的有启发性，但篇幅和水平有限，肯定没有原书好。阅读本文之前请确保自己认真读过原书对应章节或在其他书上学过类似的知识。

差不多可以开始了。由于第一章是导论，这里先忽略掉，并假设读者已经读过。本文对应章节是原书第二章第一节到2.1.6为止。主要内容是量子力学中的线性代数。

## 量子力学中的线性代数
本节意在使用量子力学的语言描述我们需要的线性代数结论。本节内容会很平凡，熟悉线性代数的读者大可在熟悉量子力学记号后快速略过。

首先明确研究对象和基本记号。线性代数的基本研究对象是**线性空间(linear space)**。

数学上对线性空间的定义如下。

设$V$是一个非空集合，$F$是一个数域，对$V$中的元素定义两个代数运算:

1. 加法，使得$\forall\alpha,\beta\in V,有\alpha+\beta\in V$;
2. 数乘，使得$\forall\alpha\in V,k\in F,有k\alpha\in V$.

并且加法和数乘满足:

1. (交换律) $\alpha+\beta=\beta+\alpha$; 
2. (结合律) $(\alpha+\beta)+\gamma=\alpha+(\beta+\gamma)$;
3. $V$中有一个零元素$\theta$，使$\forall\alpha\in V,有\alpha+\theta=\alpha$;
4. $\forall\alpha\in V,有-\alpha\in V,使\alpha+(-\alpha)=\theta$;
5. 数域$F$中的$1$，有$1\alpha=\alpha$;(这里的$1$指使$F$成为域的公理中要求的$1$元素)
6. $\forall k,l\in F,有k(l\alpha)=(kl)\alpha$;
7. (分配律) $k(\alpha+\beta)=k\alpha+k\beta$;
8. (分配律) $(k+l)\alpha=k\alpha+k\beta$.

以上$\alpha,\beta,\gamma$是$V$中的任意元素，$k,l$是$F$中的任意数。则称$V$是数域$F$上的线性空间。

我们最感兴趣的线性空间是$\mathbb{C}^n$。线性空间中的元素称为**向量(vector)**，通常使用列向量的形式表示$\mathbb{C}^n$中的向量:
$$\begin{bmatrix}
z_1\\z_2\\\vdots\\z_n
\end{bmatrix}$$
$\mathbb{C}^n$中有向量加法、数乘和零向量(记作0)。

接下来我们介绍量子力学中的标准记号——**狄拉克符号(Dirac notation)**。我们将一个向量记为一个**右矢(ket)**:
$$|\psi\rangle$$
在这一记号中，$\psi$是这个向量的名称，$|\cdot\rangle$记号表示这个对象是一个向量。对于零向量，我们用$0$来表示，而不是$|0\rangle$，后者表示一个名称为“0”的向量，我们后面会经常用到。

向量空间$V$的**子空间**$W$是$V$的一个子集，它也是向量空间，即对加法和数乘封闭。

今后如果不加特殊说明，线性空间都指复数域$\mathbb{C}$上的线性空间，特别的，通常只需要考虑$\mathbb{C}^n$。

### 基与线性无关
称一组向量$|v_1\rangle,\dots,|v_n\rangle$是线性空间的**生成集合(spanning set)**，如果空间中任一向量$|v\rangle$可以写成这组向量的线性组合形式，即$|v\rangle=\sum_ia_i|v_i\rangle$。

称一组非零向量**线性相关(linear dependent)**，如果存在一组数$a_i$，其中至少有一个不为0，使得
$$a_1|v_1\rangle+a_2|v_2\rangle+\dots+a_n|v_n\rangle=0$$
称一组非零向量**线性无关(linear independent)**，如果它们不是线性相关的。

称一组非零向量是线性空间的一组**基(basis)**，如果它们既是生成集合，又线性无关。

定义线性空间的**维数(dimension)**为它的一组基含有的向量个数，记作$\dim V$。可以证明，如果线性空间存在一组有限基，基中向量个数为$n$，那么它的所有基向量个数都为$n$。所以有限维数是良定义的。我们目前只需要考虑有限维空间。

### 线性算子和矩阵
对于映射$A:V\rightarrow W$，称$A$是一个从$V$到$W$的**线性算子(linear operator)**，如果$A$有线性，即
$$A(\sum_i a_i|v_i\rangle)=\sum_i a_iA(|v_i\rangle)$$
通常将$A(|v\rangle)$记作$A|v\rangle$。

称$A$是一个$V$上的线性算子，如果$A$是一个从$V$到$V$的线性算子。

$V$上的恒等算子记作$I_V$，有$I_V|v\rangle\equiv|v\rangle$，在不至于引起歧义的情况下记作$I$。

零算子记作$0$，有$0|v\rangle\equiv0$。

设$A:V\rightarrow W,B:W\rightarrow X$，用$BA$表示它们的复合，即有$(BA)(|v\rangle)=B(A(|v\rangle))$。通常简记为$BA|v\rangle$。

理解线性算子最方便的方式，是把它表示为**矩阵**。事实上，二者是等价的关系。我们分别从两个方向考虑一下。

给定两个线性空间$V,W$,其中$|v_1\rangle,\dots,|v_n\rangle$和$|w_m\rangle,\dots,|w_n\rangle$分别是$V$和$W$的一组基，以及给定一个线性算子$A$。我们有
$$A|v_j\rangle=\sum_i A_{ij}|w_i\rangle$$
其中$A_{ij}$是一个复数。那么矩阵$(A_{ij})$就能够表示这个给定的线性算子。

同理给定一个矩阵和两个线性空间和它们的一组基，我们就能够描述出一个线性算子，读者可以自行写出显式的形式。

不难证明，线性算子的复合就是矩阵的乘法，单位算子就是单位矩阵。

由此，我们得到了线性算子的等价表示形式——矩阵。今后我们对线性算子和矩阵不加以区分(注意要给定线性空间中的基，而我们最感兴趣的$\mathbb{C}^n$中有自然基)。

### 泡利矩阵
**泡利矩阵(the Pauli matrics)**是几个**非常有用**的$2\times2$矩阵。我们今后会发现它们有很多非常好的性质。请务必牢记于心。

$$\sigma_0\equiv I\equiv\begin{bmatrix}
    1 & 0 \\
    0 & 1
\end{bmatrix}$$
$$\sigma_1\equiv\sigma_x\equiv X\equiv\begin{bmatrix}
    0 & 1 \\
    1 & 0
\end{bmatrix}$$
$$\sigma_2\equiv\sigma_y\equiv Y\equiv\begin{bmatrix}
    0 & -i \\
    i & 0
\end{bmatrix}$$
$$\sigma_3\equiv\sigma_z\equiv Z\equiv\begin{bmatrix}
    1 & 0 \\
    0 & -1
\end{bmatrix}$$
矩阵左面是它的几种等价符号。我们之后会慢慢介绍它们的性质。

### 内积
给定线性空间$V$中的两个向量$|v\rangle, |w\rangle$，我们可以定义它们的**内积(inner product)**，结果是一个复数。我们采用符号$(|v\rangle,|w\rangle)$表示$|v\rangle$和$|w\rangle$的内积。内积的严格定义如下。

称函数$(\cdot,\cdot):V\times V\rightarrow\mathbb{C}$是内积，如果它满足以下条件:

1. $(\cdot,\cdot)$在第二个参数上有线性，即
$$(|v\rangle,\sum_i \lambda_i|w_i\rangle)=\sum_i \lambda_i(|v\rangle,|w_i\rangle).$$
2. $(|v\rangle, |w\rangle)=(|w\rangle,|v\rangle)^*$.
3. $(|v\rangle, |v\rangle)\geq0$，当且仅当$|v\rangle=0$时取等号。

其中$z^*$指复数$z$的复共轭。定义了内积的线性空间称为**内积空间(inner product space)**。

例如，$\mathbb{C}^n$中可以将内积定义为
$$(\begin{bmatrix}y_1\\\vdots\\y_n\end{bmatrix},\begin{bmatrix}z_1\\\vdots\\z_n\end{bmatrix})\equiv\sum_iy_i^*z_i=[y_1^*\dots y_n^*]\begin{bmatrix}z_1\\\vdots\\z_n\end{bmatrix}$$
读者最好自行验证一遍这个定义满足内积公理。

内积的一个平凡却常用的性质是$(\cdot,\cdot)$在第一个参数上有共轭线性，即
$$(\sum_i\lambda_i|v_i\rangle,|w\rangle)=\sum_i\lambda_i^*(|v_i\rangle,|w\rangle)$$
读者自证不难。

符号$(\cdot,\cdot)$不是量子力学中的标准记号，通常我们将$|v\rangle$和$|w\rangle$的内积$(|v\rangle,|w\rangle)$表示为$\langle v|w\rangle$，并且使用记号$\langle v|$表示$|v\rangle$的**对偶向量(dual vector)**，它是一个从内积空间$V$到复数域$\mathbb{C}$的线性算子，定义为$\forall |w\rangle\in V,\langle v|(|w\rangle)\equiv\langle v|w\rangle\equiv(|v\rangle, |w\rangle)$。从上面的例子中我们可以看到，$\mathbb{C}^n$中对偶向量的矩阵表示就是一个行向量，而且可以视为原向量的共轭转置。对偶向量全体构成的空间叫**对偶空间(dual spqce)**，记为$V^*$。事实上，对偶空间就是从$V$到$F$的所有线性算子的集合(为什么？)。容易验证，$V^*$也是一个线性空间，而且有$(|v\rangle^*)^*\equiv|v\rangle$，所以$(V^*)^*\equiv V$。

类似地，使用记号$\langle v|A|w\rangle$表示$(|v\rangle, A|w\rangle)$，其中A是一个从$W$到$V$的线性算子，$|w\rangle\in W,|v\rangle\in V$。

>与右矢(ket)对应，记号$\langle\cdot|$称为**左矢(bra)**，不要想歪，二者只是bracket(括号)的拆分。
量子力学最关注的空间是**希尔伯特空间(Hilbert space)**，也就是完备的内积空间，其中的完备性指柯西列收敛。任何有限维内积空间都是希尔伯特空间，而我们暂时只对有限维感兴趣，所以如不加说明，我们假设之后提到的希尔伯特空间都指有限维复内积空间。
>数学上对希尔伯特空间的定义过程更加有趣一些，理解这一过程对理解为什么我们需要希尔伯特空间很有帮助。线性空间之前已经定义过，是具有线性结构的空间。另一个基本的空间是度量空间(metric space)，是具有度量结构的空间，简言之定义了一个满足正定性、对称性、三角不等式的二元实值函数。接下来考虑给线性空间更好的性质。为了度量“长度”，在线性空间中引入了范数的概念，即满足正定性、齐次性、三角不等式的一元实值函数，这样的空间称为赋范线性空间(normed linear space)。注意到可以用范数诱导出度量，所以赋范线性空间既是线性空间，又是度量空间。为了度量“角度”，引入内积的概念，定义如上。注意到可以用内积诱导范数(自己和自己的内积开根号)，因此内积空间一定是赋范线性空间。为了研究收敛性，定义完备，即任一柯西列收敛。当然柯西列并不能定义在一般的线性空间上。通常柯西列是定义在度量空间上的。完备的赋范线性空间是巴拿赫空间(Banach space)，完备的内积空间是希尔伯特空间。因此我们知道，希尔伯特空间就是一个完备的能够度量长度、角度的线性空间。我们在介绍量子力学基本假设之后会讨论为什么我们对希尔伯特空间如此感兴趣。如果想更详细地了解细节并见识更多的例子，欢迎选修实分析:)
两个向量是**正交(orthogonal)**的，如果它们的内积为0。

定义向量$|v\rangle$的**范数(norm)**为
$$\||v\rangle\|\equiv\sqrt{\langle v|v\rangle}$$
范数为1的向量称为**单位向量(unit vector)**。一个非零向量除以它的范数称为一个单位向量的过程称为**标准化(normalize)**。

一组向量$|i\rangle$是标准正交的，如果它们都是单位向量，且两两正交。即$\langle i|j\rangle = \delta_{ij}$，其中$\delta_{ij}=1$当且仅当$i=j$，$\delta_{ij}=0$当且仅当$i\neq j$。如果一组标准正交的向量还是一组基，那么称这组向量为线性空间的标准正交基。

注意这里我们为了简便，将本应作为下标的$i$当成了这个向量的名字，而省略了可有可无的$v$等。这是标准正交基的习惯表示。

对于任意一组基，我们有**施密特正交化(Schmidt orthogonalization)**，可以得到一组标准正交基。因此任一有限维线性空间都有标准正交基。施密特正交化的过程可以在任何一本线性代数的教材中找到，因为后面用不到，这里不再赘述。只需注意一点，施密特正交化的过程对第一个向量只改变了长度，所以对于任一单位向量，可以找到含有这一向量的标准正交基。进一步，如果前k个向量是标准正交的，那么施密特正交化不会改变这k个向量，所以给定任意标准正交的向量，可以找到含有这些向量的标准正交基。

在这之后，我们对一个线性算子的矩阵表示，都是在给定两个空间的标准正交基下的矩阵表示。如果定义域值域空间相同，在不加说明的情况下选定相同的标准正交基。

考虑一个希尔伯特空间上两个向量$|w\rangle=\sum_iw_i|i\rangle,|v\rangle=\sum_jv_j|j\rangle$是在同一组标准正交基下的分解，由于$\langle i|j\rangle=\delta_{ij}$，我们有
$$\begin{aligned}\langle v|w\rangle&=\sum_{i,j}v_j^*w_i\delta_{ij}=\sum_iv_i^*w_i\\&=[v_1^*\dots v_n^*]\begin{bmatrix}w_1\\\vdots\\w_n\end{bmatrix}\end{aligned}$$

因此由于标准正交基的引入，我们可以使用列向量表示任意复线性空间的向量，使用行向量表示其对偶向量，它们的乘积表示内积。

有一种很常用的利用内积表示线性算子的方法，被称为线性算子的**外积表示(outer product representation)**。假设$|v\rangle$是线性空间$V$中的一个向量，$|w\rangle$是线性空间$W$中的一个向量，定义$|w\rangle\langle v|$是一个从$V$到$W$的线性算子，定义为
$$(|w\rangle\langle v|)(|v'\rangle)\equiv|w\rangle\langle v|v'\rangle=\langle v|v'\rangle|w\rangle$$
从这里可以一窥狄拉克符号的便利性。$|w\rangle\langle v|v'\rangle$既可以解释为线性算子$|w\rangle\langle v|$作用在向量$|v'\rangle$上，又可以解释为复数$\langle v|v'\rangle$乘上向量$|w\rangle$。可以通过矩阵乘法的结合性理解这种结合性。

如果读者熟悉矩阵的秩，会发现$|w\rangle\langle v|$对应的矩阵的秩一定为1。为了表示更复杂的线性算子，我们可以将多个这样的简单算子的进行线性组合。定义$\sum_ia_i|w_i\rangle\langle v_i|$是这样的线性算子
$$(\sum_ia_i|w_i\rangle\langle v_i|)|v'\rangle\equiv\sum_ia_i|w_i\rangle\langle v_i|v'\rangle$$

线性算子的外积表示对正交向量有**完备性关系(completeness relation)**(我自己瞎翻译的，如果有标准的翻译求指正)。我们考虑$|i\rangle$是线性空间$V$的一组标准正交基，所以$V$中任意向量$|v\rangle$都可以表示为$|v\rangle=\sum_i v_i|i\rangle$。注意到$\langle i|v\rangle=v_i$，因此有
$$(\sum_i |i\rangle\langle i|)|v\rangle=\sum_i|i\rangle\langle i|v\rangle=\sum_i v_i|i\rangle=|v\rangle$$
由于$|v\rangle$的任意性，我们有
$$\sum_i|i\rangle\langle i|=I$$
这一等式就称为完备性关系。完备性关系的一个应用是推导任意线性算子都可以表示为外积形式。考虑线性算子$A:V\rightarrow W$，$|v_i\rangle$是$V$的一组标准正交基，$|w_j\rangle$是$W$的一组标准正交基，于是我们有
$$\begin{aligned}
A&=I_VAI_W\\
&=(\sum_i |v_i\rangle\langle v_i|)A(\sum_j |w_j\rangle\langle w_j|)\\
&=\sum_{i,j}|v_i\rangle\langle v_i|A|w_j\rangle\langle w_j|\\
&=\sum_{i,j}\langle v_i|A|w_j\rangle|v_j\rangle\langle w_j|
\end{aligned}$$

完备性关系的另一个应用是**柯西-施瓦茨不等式(The Cauchy-Schwarz inequality)**。
$$|\langle v|w\rangle|^2\leq\langle v|v\rangle\langle w|w\rangle$$
证明需要一些技巧。考虑单位向量$|w\rangle/\sqrt{\langle w|w\rangle}$，可以找到含有这一单位向量的标准正交基(施密特正交化)。于是我们有
$$\begin{aligned}
\langle v|v\rangle\langle w|w\rangle&=\sum_i\langle v|i\rangle\langle i|v\rangle\langle w|w\rangle\\
&\geq\frac{\langle v|w\rangle\langle w|v\rangle}{\langle w|w\rangle}\langle w|w\rangle\\
&=\langle v|w\rangle\langle w|v\rangle\\
&=|\langle v|w\rangle|^2
\end{aligned}$$
第二步丢弃了一些正项。因此取等号当且仅当存在一个数域中的数$z$，使得$|v\rangle=z|w\rangle$或$|w\rangle=z|v\rangle$，即它们线性相关。

### 本征值与本征向量
一个线性空间$V$上的线性算子$A$的**本征向量(eigenvector)**$|v\rangle$是$V$上的一个非零向量，满足$A|v\rangle=v|v\rangle$，其中$v$是一个复数，称为$A$对$|v\rangle$的**本征值(eigenvalue)**。读者可能更熟悉特征值和特征向量这样的翻译，不过在量子力学中，通常将eigenvalue和eigenvector译作本征值和本征向量。

$A$的本征值是方程$\det|A-\lambda I|=0$的解。$\det$是矩阵的行列式。

容易验证对应本征值$v$的所有本征向量构成的集合构成一个子空间，称为$v$的本征子空间。

一个线性算子的**对角表示(diagonal representation)**为$\sum_i\lambda_i|i\rangle\langle i|$，其中$|i\rangle$是$A$的一组标准正交的本征向量。一个线性算子称为**可对角化的(diagonalizable)**如果有对角表示。下一节我们会给出希尔伯特空间中可对角化的充分必要条件。

称一个本征子空间是**简并的(degenerate)**，如果维数大于1。也可称两个本征向量是简并的，如果它们线性无关且有相同的本征值。

### 伴随和埃尔米特算子
假设$A$是线性空间$V$上的线性算子，可以证明存在唯一的线性算子$A^\dag$满足
$$(|v\rangle,A|w\rangle)=(A^\dag|v\rangle,|w\rangle)$$
其中$|v\rangle$和$|w\rangle$是$V$中的任意向量。$A^\dag$称为$A$的**伴随(adjoint)或埃尔米特共轭(Hermitian conjugate)**。定义$|v\rangle^\dag=\langle v|。$下面罗列一些埃尔米特共轭的平凡性质，请读者自行证明。
$$(AB)^\dag=B^\dag A^\dag$$
$$(A|v\rangle)^\dag=\langle v|A^\dag$$
$$(|w\rangle\langle v|)^\dag=|v\rangle\langle w|$$
$$(\sum_ia_iA_i)^\dag=\sum_ia_i^*A_i^\dag$$
$$(A^\dag)^\dag=A$$

对于矩阵表示，埃尔米特共轭等价于共轭转置，即$A^\dag=(A^*)^T$，其中$*$表示复共轭。

伴随等于自身的算子称为**埃尔米特算子(Hermitian operator)**或**自伴算子(self-adjoint operator)**。一类重要的埃尔米特算子为**投影算子(projector)**。假设$V$是一个$d$维线性空间，$W$是$V$的k维线性子空间。由施密特正交化，可以构造出$V$的一组标准正交基$|1\rangle,\dots,|d\rangle$，其中$|1\rangle,\dots,|k\rangle$是$W$的标准正交基。定义$V$上的线性算子
$$P\equiv\sum_{i=1}^k|i\rangle\langle i|$$
称$P$为$V$到$W$的投影算子。容易验证定义和标准正交基的选择无关，只和空间$V$和$W$有关。对于任意向量$|v\rangle$，$|v\rangle\langle v|$一定是埃尔米特的，故$P$一定是埃尔米特的。之后我们使用“线性空间$P$”来代表投影算子$P$投影到的子空间。算子$Q\equiv I-P$称为$P$的**正交补(orthogonal complement)**。显然线性空间$Q$是向量$|k+1\rangle,\dots,|d\rangle$生成的子空间，称为线性空间$P$的**正交补**。投影算子$P$有性质$P^2=P$，因此$P^n=P,n\in\mathbb{Z}^+$

一个算子$A$称为**正规(normal)算子**，如果$AA^\dag=A^\dag A$。显然埃尔米特算子一定是正规的。一个重要的结论是，线性算子可对角化当且仅当它是正规的，这称为**谱分解(spectral decomposition)**。证明较为繁琐，我不想敲一遍，可以自行谷歌正规矩阵的谱定理。注意到埃尔米特算子一定都是正规的，所以可以进行谱分解。同时注意到一个正规矩阵是埃尔米特的当且仅当本征值都是实的。

一个算子$U$称为**酉(unitary)算子**，如果$U^\dag U=I$。类似的一个矩阵称为酉矩阵，如果$U^\dag U=I$。容易验证酉算子也满足$UU^\dag=I$，所以酉算子也是正规的，有谱分解。酉算子的一个重要性质是它保内积，即$(U|v\rangle,U|w\rangle)=\langle v|U^\dag U|w\rangle=\langle v|I|w\rangle=\langle v|w\rangle=(|v\rangle,|w\rangle)$。因此可以将酉算子写成漂亮的外积形式。设$|v_i\rangle$是一组标准正交基，$|w_i\rangle\equiv U|v_j\rangle$，由于酉算子保内积，所以$|w_i\rangle$也是一组标准正交基。于是$U=\sum_i|w_i\rangle\langle v_i|$。相对的，对于任意两组标准正交基$|v_i\rangle,|w_i\rangle$，容易验证算子$U\equiv\sum_i|w_i\rangle\langle v_i|$是一个酉算子。容易证明，酉算子的本征值的模都为1，即可以写成$e^{i\theta}$的形式

一个算子$A$称为**正(positive)算子**，如果对于任意向量$|v\rangle$，有$\langle v|A|v\rangle$是一个非负实数。如果$\langle v|A|v\rangle$始终是一个严格正数，称其为**正定(positive definite)算子**。正算子一定是埃尔米特的，因此可以进行谱分解，而且本征值一定都是非负的。对于任意算子$A$，$A^\dag A$都是正算子。

总结一下我们定义的几类算子和它们的关系。我们的主要研究对象都是正规算子。正规算子可以进行谱分解，也就是可以对角化，它对本征值没有要求。这里的对角化实际上是酉对角化，注意与学习线性代数时的相似对角化加以区分，酉对角化要求本征向量正交，而相似对角化不需要。埃尔米特算子、酉算子、正算子、投影算子都是正规算子，因此也可以进行对角化。它们的区别仅在于本征值的要求不同。埃尔米特算子要求本征值都是实的，酉算子要求本征值模为1，正算子要求本征值都是非负的(正定算子要求本征值都是正的)，投影算子要求本征值是0或1。本征值决定了算子的类型，与具体的本征向量没有关系。


写到这里已经很长了，剩下的包括张量积、算子函数、交换子和奇异值分解下一篇再写吧。
Just Enjoy!

