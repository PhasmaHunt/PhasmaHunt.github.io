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