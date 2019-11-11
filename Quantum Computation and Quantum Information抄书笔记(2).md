# Quantum Computation and Quantum Information抄书笔记(2)


### 张量积
理解张量积对后面理解多量子态非常重要。个人觉得原书讲的并不算透彻，所以我会试着讲的更数学一点，所以下面暂时不使用量子力学的符号。为了省略

区分张量积和笛卡尔积是很重要的。首先定义线性空间的**笛卡尔积(Cartesian product)**。考虑两个线性空间$X$和$Y$，它们的笛卡尔积，记作$X\times Y$，是所有有序对组成的集合。即
$$X\times Y=\{(x,y)|x\in X,y\in Y\}$$
然后我们赋予$X\times Y$线性结构，定义加法和数乘
$$(x_1,y_1)+(x_2,y_2)=(x_1+x_2,y_1+y_2)\\
\lambda(x,y)=(\lambda x, \lambda y)$$
容易验证，拥有这样结构的笛卡尔积空间是线性空间。如果$X$是n维的，{}，$Y$是m维，有$X\times Y$是$n+m$维的。

之前定义的线性算子实际上就是数学语境下的线性映射。尝试推广定义多线性映射。

定义**k-线性映射(k-linear map)**：令$V_1,\dots,V_k$是线性空间。假设$f:V_1\times\dots\times V_k\rightarrow W$，满足
$$f(x_1,\dots,ax_r+by_r,\dots,x_k)\\=af(x_1,\dots,x_r\dots,x_k)+bf(x_1,\dots,y_r,\dots,x_k)$$
则称$f$为$k$-线性映射。以下考虑$k=2$时的双线性映射。

接下来我们定义张量积。有多种不同的定义张量积的方式，它们分别从不同角度揭示了张量积的特性，当然它们是等价的。

定义**张量积(tensor product)**：令$V_1,V_2$时两个线性空间。如果存在一个线性空$W$和一个双线性映射$f:V_1\times V_2\rightarrow W$满足

1. $W$可以由$f(V_1\times V_2)$即$f$的像集生成;
2. 对于任意双线性映射$g:V_1\times V_2\rightarrow Z$，$\exist\varphi:W\rightarrow Z$，使得$g=\varphi\circ f$.

让我们看一下这个定义告诉了我们什么。第一条保证了$W$是最小的包含$f$的像集的线性空间。第二条称为万有性，。