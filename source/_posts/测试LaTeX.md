---
tags:
  - 学习
date: 2026-09-15 00:40
updated: 2026-09-15 00:40
title: 测试LaTeX
---
# LaTeX 渲染测试（移动端安全版）

**定理**：设 $A \in \mathbb{R}^{n \times n}$，且 $A^T = A$。若 $\lambda \in \mathbb{C}$ 是 $A$ 的一个特征值，则 $\lambda \in \mathbb{R}$。

**证明**：

设 $v \in \mathbb{C}^n \setminus \{0\}$ 是 $A$ 对应于 $\lambda$ 的特征向量，即
$$ A v = \lambda v, \quad v \neq 0 $$

在 $\mathbb{C}^n$ 上取标准内积：
$$ \langle x, y \rangle := \sum_{i=1}^{n} x_i \overline{y_i} = \overline{y}^T x, \quad x, y \in \mathbb{C}^n $$

由 $A v = \lambda v$，有：
$$ \lambda \langle v, v \rangle = \langle \lambda v, v \rangle = \langle A v, v \rangle = v^* A v $$

另一方面，因为 $A$ 是实对称矩阵，所以：
$$ \overline{v^* A v} = (v^* A v)^* = v^* A^* v = v^* A^T v = v^* A v $$

其中 $A^* = \overline{A}^T = A^T = A$。因此 $v^* A v \in \mathbb{R}$。又：
$$ \langle v, v \rangle = \sum_{i=1}^{n} |v_i|^2 > 0 $$

故：
$$ \lambda = \frac{v^* A v}{\langle v, v \rangle} \in \mathbb{R} $$

所以 $A$ 的特征值均为实数。 $\square$

---

## 附加语法测试

行内公式：$\alpha, \beta, \Gamma, \Delta, \theta, \lambda, \mu, \pi, \sigma, \phi, \omega$。

行内测试：$a \le b \iff b \ge a$， $x \to 0^+$， $\forall x \in \mathbb{R} \ \exists n \in \mathbb{N}$。

极限、积分、求和、连乘、组合数（拆成单独的块）：
$$ \lim_{x \to 0} \frac{\sin x}{x} = 1 $$
$$ \int_{-\infty}^{+\infty} e^{-x^2} \, dx = \sqrt{\pi} $$
$$ \sum_{k=1}^{n} k^2 = \frac{n(n+1)(2n+1)}{6} $$
$$ \prod_{i=1}^{n} i = n! $$
$$ \binom{n}{k} = \frac{n!}{k!(n-k)!} $$

多行对齐（移动端建议用独立行代替 aligned）：
$$ f(x) = a_0 + a_1 x + a_2 x^2 + \cdots + a_n x^n $$
$$ f'(x) = \sum_{k=1}^{n} k a_k x^{k-1} $$

分段函数（移动端经常崩溃，改用简单写法）：
若 $x > 0$，则 $\operatorname{sgn}(x) = 1$；若 $x = 0$，则 $\operatorname{sgn}(x) = 0$；若 $x < 0$，则 $\operatorname{sgn}(x) = -1$。

矩阵（移动端安全写法，换行必须用 \\）：
$$ A = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} $$
$$ \det B = \begin{vmatrix} a & b \\ c & d \end{vmatrix} = ad - bc $$

括号、取整、集合（放弃 \Bigl，改用 \left）：
$$ \left( \frac{a}{b} \right)^n = \frac{a^n}{b^n} $$
$$ \left\{ x \in \mathbb{R} \mid |x| < 1 \right\} $$
$$ \lfloor x \rfloor \le x < \lceil x \rceil $$

花体、黑板粗体、期望、向量：
$$ \mathcal{F}(x) = \int_{-\infty}^{x} f(t) \, dt $$
$$ \mathbb{E}[X] = \sum_{\omega \in \Omega} X(\omega) \Pr(\omega) $$
$$ \vec{v} = \begin{pmatrix} v_1 \\ v_2 \\ v_3 \end{pmatrix} $$
$$ \dot{x} = \frac{dx}{dt}, \quad \ddot{x} = \frac{d^2 x}{dt^2} $$
$$ \nabla f = \left( \frac{\partial f}{\partial x_1}, \ldots, \frac{\partial f}{\partial x_n} \right) $$

极限与逻辑量词：
$$ \lim_{n \to \infty} \left( 1 + \frac{1}{n} \right)^n = e $$
$$ \forall \varepsilon > 0, \ \exists \delta > 0: \ |x - a| < \delta \implies |f(x) - f(a)| < \varepsilon $$