---
tags:
  - 学习
date: 2026-09-15 00:40
updated: 2026-09-15 00:40
title: 测试LaTeX
---
# LaTeX 渲染测试：实对称矩阵的特征值为实数

**定理**：设 $A\in\mathbb{R}^{n\times n}$，且 $A^{\mathsf T}=A$。若 $\lambda\in\mathbb{C}$ 是 $A$ 的一个特征值，则 $\lambda\in\mathbb{R}$。

**证明**：

设 $v\in\mathbb{C}^n\setminus\{\mathbf{0}\}$ 是 $A$ 对应于 $\lambda$ 的特征向量，即
$$
Av=\lambda v,\qquad v\neq \mathbf{0}.
$$
在 $\mathbb{C}^n$ 上取标准内积
$$
\langle x,y\rangle
:=\sum_{i=1}^{n}x_i\overline{y_i}
=\overline{y}^{\mathsf T}x,
\qquad x,y\in\mathbb{C}^n.
$$
由 $Av=\lambda v$，有
$$
\lambda\langle v,v\rangle
=\langle \lambda v,v\rangle
=\langle Av,v\rangle
=v^*Av.
$$
另一方面，因为 $A$ 是实对称矩阵，所以
$$
\overline{v^*Av}
=(v^*Av)^*
=v^*A^*v
=v^*A^{\mathsf T}v
=v^*Av,
$$
其中 $A^*=\overline{A}^{\mathsf T}=A^{\mathsf T}=A$。因此 $v^*Av\in\mathbb{R}$。又
$$
\langle v,v\rangle
=\sum_{i=1}^{n}|v_i|^2>0,
$$
故
$$
\lambda
=\frac{v^*Av}{\langle v,v\rangle}
\in\mathbb{R}.
$$
所以 $A$ 的特征值均为实数。$\square$

---

## 附加 LaTeX 语法测试

行内公式：$\alpha,\beta,\Gamma,\Delta,\theta,\lambda,\mu,\pi,\sigma,\phi,\omega$。

行内公式：$a\le b\iff b\ge a$，$x\to 0^+$，$\forall x\in\mathbb{R}\ \exists n\in\mathbb{N}$。

极限、积分、求和、连乘、组合数：
$$
\lim_{x\to 0}\frac{\sin x}{x}=1,\qquad
\int_{-\infty}^{+\infty}e^{-x^2}\,dx=\sqrt{\pi},\qquad
\sum_{k=1}^{n}k^2=\frac{n(n+1)(2n+1)}{6},
$$
$$
\prod_{i=1}^{n}i=n!,\qquad
\binom{n}{k}=\frac{n!}{k!(n-k)!}.
$$

多行对齐：
$$
\begin{aligned}
f(x)&=a_0+a_1x+a_2x^2+\cdots+a_nx^n\\
&=\sum_{k=0}^{n}a_kx^k,\\
f'(x)&=\sum_{k=1}^{n}k a_k x^{k-1}.
\end{aligned}
$$

分段函数：
$$
\begin{cases}
x+y=3,\\
x-y=1,
\end{cases}
\quad\Longrightarrow\quad
\begin{cases}
x=2,\\
y=1.
\end{cases}
$$

矩阵：
$$
A=\begin{pmatrix}
1 & 2 & 3\\
4 & 5 & 6\\
7 & 8 & 9
\end{pmatrix},\qquad
B=\begin{bmatrix}
a & b\\
c & d
\end{bmatrix},\qquad
\det B=\begin{vmatrix}
a & b\\
c & d
\end{vmatrix}=ad-bc.
$$

括号、取整、集合：
$$
\left(\frac{a}{b}\right)^n=\frac{a^n}{b^n},\qquad
\Bigl\{x\in\mathbb{R}\mid |x|<1\Bigr\},\qquad
\left\lfloor x\right\rfloor\le x<\left\lceil x\right\rceil.
$$

花体、黑板粗体、期望、符号函数：
$$
\mathcal{F}(x)=\int_{-\infty}^{x}f(t)\,dt,\qquad
\mathbb{E}[X]=\sum_{\omega\in\Omega}X(\omega)\Pr(\omega),\qquad
\operatorname{sgn}(x)=
\begin{cases}
1,&x>0,\\
0,&x=0,\\
-1,&x<0.
\end{cases}
$$

向量、导数、偏导、梯度：
$$
\vec{v}=\begin{pmatrix}v_1\\v_2\\v_3\end{pmatrix},\qquad
\dot{x}=\frac{dx}{dt},\qquad
\ddot{x}=\frac{d^2x}{dt^2},\qquad
\nabla f=\left(\frac{\partial f}{\partial x_1},\ldots,\frac{\partial f}{\partial x_n}\right).
$$

极限与逻辑量词：
$$
\lim_{n\to\infty}\left(1+\frac{1}{n}\right)^n=e,\qquad
\forall \varepsilon>0,\ \exists \delta>0:\ |x-a|<\delta\implies |f(x)-f(a)|<\varepsilon.
$$