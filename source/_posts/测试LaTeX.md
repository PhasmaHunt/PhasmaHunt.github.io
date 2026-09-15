---
tags:
  - 学习
date: 2026-09-15 00:40
updated: 2026-09-15 00:40
title: 测试LaTeX
---
# Stolz 定理及其证明

**定理（Stolz 定理，$\frac{*}{\infty}$ 型）**：
设数列 $\{y_n\}$ 严格单调递增，且 $\lim_{n \to \infty} y_n = +\infty$。
如果极限 $\lim_{n \to \infty} \frac{x_{n+1} - x_n}{y_{n+1} - y_n} = L$（其中 $L$ 为有限实数），
则数列 $\{x_n\}$ 满足：
$$ \lim_{n \to \infty} \frac{x_n}{y_n} = L $$

**证明**：

已知 $\lim_{n \to \infty} \frac{x_{n+1} - x_n}{y_{n+1} - y_n} = L$。
根据数列极限的定义，对任意给定的 $\varepsilon > 0$，存在正整数 $N_1$，使得当 $n > N_1$ 时，有：
$$ \left| \frac{x_{n+1} - x_n}{y_{n+1} - y_n} - L \right| < \varepsilon $$

因为 $\{y_n\}$ 严格单调递增，所以 $y_{n+1} - y_n > 0$。于是上式可以展开为：
$$ (L - \varepsilon)(y_{n+1} - y_n) < x_{n+1} - x_n < (L + \varepsilon)(y_{n+1} - y_n) $$

取定一个 $N > N_1$。对于任意 $n > N$，我们将 $x_n - x_N$ 写成差分和的形式：
$$ x_n - x_N = \sum_{k=N}^{n-1} (x_{k+1} - x_k) $$

利用前面的不等式对每一项进行放缩，得到：
$$ (L - \varepsilon) \sum_{k=N}^{n-1} (y_{k+1} - y_k) < x_n - x_N < (L + \varepsilon) \sum_{k=N}^{n-1} (y_{k+1} - y_k) $$

中间的求和式是一个 telescoping sum（裂项相消），可以直接算出：
$$ \sum_{k=N}^{n-1} (y_{k+1} - y_k) = y_n - y_N $$

因此，不等式化简为：
$$ (L - \varepsilon)(y_n - y_N) < x_n - x_N < (L + \varepsilon)(y_n - y_N) $$

将 $x_N$ 移项，得到 $x_n$ 的上下界：
$$ x_N + (L - \varepsilon)(y_n - y_N) < x_n < x_N + (L + \varepsilon)(y_n - y_N) $$

因为 $y_n \to +\infty$，所以当 $n$ 足够大时，$y_n > 0$。不等式两边同时除以 $y_n$：
$$ \frac{x_N}{y_n} + (L - \varepsilon)\left(1 - \frac{y_N}{y_n}\right) < \frac{x_n}{y_n} < \frac{x_N}{y_n} + (L + \varepsilon)\left(1 - \frac{y_N}{y_n}\right) $$

将常数项与 $n$ 相关的项分离：
$$ L - \varepsilon + \frac{x_N - (L - \varepsilon)y_N}{y_n} < \frac{x_n}{y_n} < L + \varepsilon + \frac{x_N - (L + \varepsilon)y_N}{y_n} $$

注意，$x_N$、$y_N$、$L$、$\varepsilon$ 都是固定常数。因为 $y_n \to +\infty$，所以有：
$$ \lim_{n \to \infty} \frac{x_N - (L - \varepsilon)y_N}{y_n} = 0 $$
$$ \lim_{n \to \infty} \frac{x_N - (L + \varepsilon)y_N}{y_n} = 0 $$

因此，存在正整数 $N_2 > N$，使得当 $n > N_2$ 时，这两个分式的绝对值均小于 $\varepsilon$。于是有：
$$ L - 2\varepsilon < \frac{x_n}{y_n} < L + 2\varepsilon $$

即：
$$ \left| \frac{x_n}{y_n} - L \right| < 2\varepsilon $$

由极限的定义可知：
$$ \lim_{n \to \infty} \frac{x_n}{y_n} = L $$
证毕。 $\square$
# Cauchy-Binet 定理及其证明

**定理（Cauchy-Binet 公式）**：
设 $A$ 是 $m \times n$ 矩阵，$B$ 是 $n \times m$ 矩阵。
如果 $m > n$，则矩阵乘积的行列式为零：$\det(AB) = 0$。
如果 $m \le n$，则：
$$ \det(AB) = \sum_{S \subseteq \{1, \dots, n\}, |S| = m} \det(A_S) \det(B_S) $$
其中，$S$ 是 $\{1, \dots, n\}$ 的一个包含 $m$ 个元素的子集，$A_S$ 表示取 $A$ 的列索引为 $S$ 构成的 $m \times m$ 子矩阵，$B_S$ 表示取 $B$ 的行索引为 $S$ 构成的 $m \times m$ 子矩阵。

**证明**：

我们使用行列式的莱布尼茨展开式（Leibniz formula）来证明。
令 $A$ 和 $B$ 的具体形式如下：
$$ A = \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \cdots & a_{mn} \end{pmatrix} $$
$$ B = \begin{pmatrix} b_{11} & b_{12} & \cdots & b_{1m} \\ b_{21} & b_{22} & \cdots & b_{2m} \\ \vdots & \vdots & \ddots & \vdots \\ b_{n1} & b_{n2} & \cdots & b_{nm} \end{pmatrix} $$

根据行列式定义，$m \times m$ 矩阵 $AB$ 的行列式可展开为：
$$ \det(AB) = \sum_{\sigma \in S_m} \operatorname{sgn}(\sigma) \prod_{i=1}^{m} (AB)_{i, \sigma(i)} $$

其中 $S_m$ 是所有 $m$ 阶排列的集合，$(AB)_{i, \sigma(i)}$ 是矩阵 $AB$ 的第 $i$ 行第 $\sigma(i)$ 列的元素。
由矩阵乘法定义可知：
$$ (AB)_{i, \sigma(i)} = \sum_{k=1}^{n} a_{i,k} b_{k, \sigma(i)} $$

代入行列式的展开式中，得到：
$$ \det(AB) = \sum_{\sigma \in S_m} \operatorname{sgn}(\sigma) \prod_{i=1}^{m} \left( \sum_{k_i=1}^{n} a_{i, k_i} b_{k_i, \sigma(i)} \right) $$

将乘积展开，并交换求和顺序（将关于 $k_i$ 的求和提到最外层）：
$$ \det(AB) = \sum_{k_1=1}^{n} \cdots \sum_{k_m=1}^{n} \left( \prod_{i=1}^{m} a_{i, k_i} \right) \left( \sum_{\sigma \in S_m} \operatorname{sgn}(\sigma) \prod_{i=1}^{m} b_{k_i, \sigma(i)} \right) $$

现在考察最内层的求和：$\sum_{\sigma \in S_m} \operatorname{sgn}(\sigma) \prod_{i=1}^{m} b_{k_i, \sigma(i)}$。
如果下标 $k_1, k_2, \dots, k_m$ 中存在重复，由于 $b_{k_i, \sigma(i)}$ 有两行完全相同（对应重复的下标），该行列式展开值为 $0$。
因此，我们只需要考虑 $k_1, k_2, \dots, k_m$ 互不相同的情况。此时，它们构成了一个集合 $S = \{k_1, \dots, k_m\} \subseteq \{1, \dots, n\}$，且 $|S| = m$。

设 $S$ 中的元素按升序排列为 $s_1 < s_2 < \cdots < s_m$。
由于 $k_1, \dots, k_m$ 是 $S$ 的一个排列，存在唯一的排列 $\tau \in S_m$，使得 $k_i = s_{\tau(i)}$。
将 $k_i = s_{\tau(i)}$ 代入内层求和：
$$ \sum_{\sigma \in S_m} \operatorname{sgn}(\sigma) \prod_{i=1}^{m} b_{s_{\tau(i)}, \sigma(i)} $$

令 $j = \tau(i)$，则 $i = \tau^{-1}(j)$，令 $\rho = \sigma \circ \tau^{-1}$。此时 $\rho$ 也是 $S_m$ 中的排列，且 $\operatorname{sgn}(\sigma) = \operatorname{sgn}(\rho) \operatorname{sgn}(\tau)$。
内层求和化简为：
$$ \operatorname{sgn}(\tau) \sum_{\rho \in S_m} \operatorname{sgn}(\rho) \prod_{j=1}^{m} b_{s_j, \rho(j)} = \operatorname{sgn}(\tau) \det(B_S) $$

这里 $\det(B_S)$ 正是由 $B$ 的第 $s_1, \dots, s_m$ 行构成的 $m \times m$ 子矩阵的行列式：
$$ B_S = \begin{pmatrix} b_{s_1, 1} & b_{s_1, 2} & \cdots & b_{s_1, m} \\ b_{s_2, 1} & b_{s_2, 2} & \cdots & b_{s_2, m} \\ \vdots & \vdots & \ddots & \vdots \\ b_{s_m, 1} & b_{s_m, 2} & \cdots & b_{s_m, m} \end{pmatrix} $$

将内层求和的结果代回最外层的求和式中，我们得到：
$$ \det(AB) = \sum_{|S|=m} \sum_{\tau \in S_m} \left( \prod_{i=1}^{m} a_{i, s_{\tau(i)}} \right) \operatorname{sgn}(\tau) \det(B_S) $$

注意到 $\det(B_S)$ 与排列 $\tau$ 无关，可以将其提到 $\sum_{\tau}$ 的外面：
$$ \det(AB) = \sum_{|S|=m} \det(B_S) \left( \sum_{\tau \in S_m} \operatorname{sgn}(\tau) \prod_{i=1}^{m} a_{i, s_{\tau(i)}} \right) $$

观察括号内的部分，它正是由 $A$ 的第 $s_1, \dots, s_m$ 列构成的 $m \times m$ 子矩阵 $A_S$ 的行列式：
$$ A_S = \begin{pmatrix} a_{1, s_1} & a_{1, s_2} & \cdots & a_{1, s_m} \\ a_{2, s_1} & a_{2, s_2} & \cdots & a_{2, s_m} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m, s_1} & a_{m, s_2} & \cdots & a_{m, s_m} \end{pmatrix} $$
因此：
$$ \sum_{\tau \in S_m} \operatorname{sgn}(\tau) \prod_{i=1}^{m} a_{i, s_{\tau(i)}} = \det(A_S) $$

最终，我们得出结论：
$$ \det(AB) = \sum_{S \subseteq \{1, \dots, n\}, |S| = m} \det(A_S) \det(B_S) $$
证毕。 $\square$
