---
tags:
  - 学习
  - 笔记
  - 算法
date: 2026-10-9 02:00
updated: 2026-10-9 02:00
title: 【OI Wiki】1.数据结构
---
~~模板刷题记~~
## 0. 数组

### STL : `vector`

``` cpp
vector<int> a;
vector<int> a(100);
vector<int> a(100, 1);

vector<vector<int>> a(100, vector<int> ());
vector<vector<int>> a(100, vector<int> (200, 0));

a.push_back(1); // O(1)
a.pop_back(); // O(1)

int t = a[1]; // O(1)
int t = a.back(); // O(1)

int siz = a.size(); // O(1)
a.clear(); // O(n)
bool emp = a.empty(); // O(1)
```

## 1. 栈、队列

### STL : `deque`

``` cpp
deque<int> a;
deque<int> a(100);
deque<int> a(100, 1);

a.push_back(1); // O(1)
a.pop_back(); // O(1)
a.push_front(1); // O(1)
a.pop_front(); // O(1)

int siz = a.size(); // O(1)
a.clear(); // O(n)
bool emp = a.empty(); // O(1)
```

## 2. 链表

### 实现（单向链表）

``` cpp
struct node
{ 
	int value; 
	node *next; 
};

void insertn(int i, node *p)
{
	node *n = new node;
	n->value = i;
	n->next = p->next;
	p->next = n;
}

void deleten(node *p)
{
	node *t = p->next;
	p->value = t->value;
	p->next = t->next;
	delete t;
}
```

## 3. 单调栈

### 实现

```cpp
deque<int> a();
int x;

// insert x
while (!a.empty() and a.back()<x)
{
    a.pop_back();
}
a.push_back(x);
```

### 例题：【模板】单调栈

> **题目链接**：[Luogu P5788](https://www.luogu.com.cn/problem/P5788)
>
> **题目描述**
>
> 给出项数为 $n$ 的整数数列 $a_{1 \dots n}$。
>
> 定义函数 $f(i)$ 代表数列中第 $i$ 个元素之后第一个大于 $a_i$ 的元素的**下标**，即 $f(i)=\min_{i<j\leq n, a_j > a_i} \{j\}$。若不存在，则 $f(i)=0$。
>
> 试求出 $f(1\dots n)$。
>
> **输入格式**
>
> 第一行一个正整数 $n$。
>
> 第二行 $n$ 个正整数 $a_{1\dots n}$。
>
> **输出格式**
>
> 一行 $n$ 个整数表示 $f(1), f(2), \dots, f(n)$ 的值。
>
> **数据范围**
>
> - 对于 $30\%$ 的数据，$n\leq 100$；
> - 对于 $60\%$ 的数据，$n\leq 5 \times 10^3$；
> - 对于 $100\%$ 的数据，$1 \le n\leq 3\times 10^6$，$1\leq a_i\leq 10^9$。
> 

#### Code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

void solve()
{
    ll n, input;
    cin >> n;
    vector<ll> f(n, 0);
    deque<pair<ll, ll>> d;
    for (ll i = 0; i < n; ++i)
    {
        cin >> input;
        while (!d.empty() and d.back().first < input)
        {
            f[d.back().second] = i + 1;
            d.pop_back();
        }
        d.push_back(pair(input, i));
    }
    for (ll i = 0; i < n; ++i)
        cout << f[i] << " ";
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

## 4. 单调队列

### 例题：【模板】单调队列

> **题目链接**：[Luogu P1886](https://www.luogu.com.cn/problem/P1886)
>
> **题目描述**
>
> 有一个长为 $n$ 的序列 $a$，以及一个大小为 $k$ 的窗口。现在这个窗口从左边开始向右滑动，每次滑动一个单位，求出每次滑动后窗口中的最小值和最大值。
>
> 例如，对于序列 $[1,3,-1,-3,5,3,6,7]$ 以及 $k = 3$，有如下过程：
>$$\def\arraystretch{1.2}
\begin{array}{|c|c|c|}\hline
\textsf{窗口位置} & \textsf{最小值} & \textsf{最大值} \\ \hline
\verb![1   3  -1] -3   5   3   6   7 ! & -1 & 3 \\ \hline
\verb! 1  [3  -1  -3]  5   3   6   7 ! & -3 & 3 \\ \hline
\verb! 1   3 [-1  -3   5]  3   6   7 ! & -3 & 5 \\ \hline
\verb! 1   3  -1 [-3   5   3]  6   7 ! & -3 & 5 \\ \hline
\verb! 1   3  -1  -3  [5   3   6]  7 ! & 3 & 6 \\ \hline
\verb! 1   3  -1  -3   5  [3   6   7]! & 3 & 7 \\ \hline
\end{array}
$$
> **输入格式**
>
> 输入一共有两行，第一行有两个正整数 $n,k$；
>
> 第二行有 $n$ 个整数，表示序列 $a$。
>
> **输出格式**
>
> 输出共两行，第一行为每次窗口滑动的最小值；
>
> 第二行为每次窗口滑动的最大值。
>
> **数据范围**
>
> - 对于 $50\%$ 的数据，$1 \le n \le 10^5$；
> - 对于 $100\%$ 的数据，$1\le k \le n \le 10^6$，$a_i \in [-2^{31},2^{31})$。
> 

#### Code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

void solve()
{
    ll n, k, input;
    cin >> n >> k;
    vector<ll> a(n);
    for (ll i = 0; i < n; ++i)
        cin >> a[i];
    deque<pair<ll, ll>> d;
    for (ll i = 0; i < n; ++i)
    {
        input = a[i];
        while (!d.empty() and d.back().first > input)
        {
            d.pop_back();
        }
        d.push_back(pair(input, i));
        if(d.front().second<=i-k){
            d.pop_front();
        }
        if(i>=k-1)
            cout<<d.front().first<<" ";
    }
    d.clear();
    cout<<"\n";
    for (ll i = 0; i < n; ++i)
    {
        input = a[i];
        while (!d.empty() and d.back().first < input)
        {
            d.pop_back();
        }
        d.push_back(pair(input, i));
        if(d.front().second<=i-k){
            d.pop_front();
        }
        if(i>=k-1)
            cout<<d.front().first<<" ";
    }
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

## 5. 二叉堆

### 实现

考虑使用一个序列 $h$ 来表示堆， $h_i$ 的两个儿子分别是 $h_{2i}$ 和 $h_{2i+1}$ ，1是根结点。
**向上调整：** 如果结点的值大于它父亲的值，就交换，重复此过程直到不满足或者到根。
**向下调整：** 在该结点的儿子中，找一个值最大的，与该结点交换，重复此过程直到底层。
**插入操作：** 从最下一层最右边的叶子之后插入，再对其向上调整。
**删除操作：** 删除堆中最大的元素，即删除根结点。把根结点和最后一个结点直接交换，直接删掉最后一个结点，再对新根节点向下调整。

```cpp
void up(int x)
{
  while (x > 1 and h[x] > h[x / 2])
  {
    swap(h[x], h[x / 2]);
    x /= 2;
  }
}

void down(int x)
{
  while (x * 2 <= n)
  {
    t = x * 2;
    if (t + 1 <= n and h[t + 1] > h[t]) t++;
    if (h[t] <= h[x]) break;
    swap(h[x], h[t]);
    x = t;
  }
}
```

### STL : `priority_queue`

``` cpp
priority_queue<int> pq; // 大顶堆 等价于priority_queue<int, std::vector<int>, std::less<int>> pq;
priority_queue<int, vector<int>, greater<int>> min_pq; // 小顶堆

pq.push(x);        // O(log n)
pq.top();          // O(1)
pq.pop();          // O(log n)
pq.empty();
pq.size();

//自定义比较
auto cmp = [](ll a, ll b)
{
    return a > b;
};
priority_queue<ll, vector<ll>, decltype(cmp)> pq;
```

### 例题：【模板】堆

> **题目链接**：[Luogu P3378](https://www.luogu.com.cn/problem/P3378)
>
> **题目描述**
>
> 给定一个数列，初始为空，请支持下面三种操作：
>
> 1. 给定一个整数 $x$，请将 $x$ 加入到数列中。
> 2. 输出数列中最小的数。
> 3. 删除数列中最小的数（如果有多个数最小，只删除 $1$ 个）。
>
> **输入格式**
>
> 第一行是一个整数，表示操作的次数 $n$。
>
> 接下来 $n$ 行，每行表示一次操作。每行首先有一个整数 $op$ 表示操作类型。
>
> - 若 $op = 1$，则后面有一个整数 $x$，表示要将 $x$ 加入数列。
> - 若 $op = 2$，则表示要求输出数列中的最小数。
> - 若 $op = 3$，则表示删除数列中的最小数。如果有多个数最小，只删除 $1$ 个。
>
> **输出格式**
>
> 对于每个操作 $2$，输出一行一个整数表示答案。
>
> **数据范围**
>
> - 对于 $30\%$ 的数据，保证 $n \leq 15$。
> - 对于 $70\%$ 的数据，保证 $n \leq 10^4$。
> - 对于 $100\%$ 的数据，保证 $1 \leq n \leq 10^6$，$1 \leq x < 2^{31}$，$op \in \{1, 2, 3\}$。
>

#### Code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

void solve()
{
    ll leng = 0, T, op, nums;
    cin >> T;
    vector<ll> h(1, 0);
    auto up = [&](ll x)
    {
        while (x > 1 and h[x] < h[x / 2])
        {
            swap(h[x], h[x / 2]);
            x /= 2;
        }
    };
    auto down = [&](ll x)
    {
        while (x * 2 <= leng)
        {
            ll t = x * 2;
            if (t + 1 <= leng and h[t + 1] < h[t])
                t++;
            if (h[t] >= h[x])
                break;
            swap(h[x], h[t]);
            x = t;
        }
    };
    while (T--)
    {
        cin >> op;
        if (op == 1)
        {
            leng++;
            cin >> nums;
            h.push_back(nums);
            up(leng);
        }

        else if (op == 2)
        {
            cout << h[1] << "\n";
        }
        else if (op == 3)
        {
            swap(h[1], h[leng]);
            h.pop_back();
            leng--;
            down(1);
        }
    }
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

#### Code (STL)

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

void solve()
{
    auto cmp = [](ll a, ll b)
    {
        return a > b;
    };
    priority_queue<ll, vector<ll>, decltype(cmp)> pq;
    ll T, op, nums;
    cin >> T;
    while (T--)
    {
        cin >> op;
        if (op == 1)
        {
            cin >> nums;
            pq.push(nums);
        }
        else if (op == 2)
        {
            cout << pq.top() << "\n";
        }
        else if (op == 3)
        {
            pq.pop();
        }
    }
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

## 6. 并查集

### 问题

实现对输入元素所属集合的合并和查询的功能。

### 实现

使用一个森林，其中每棵树表示一个集合，树中的节点表示对应集合中的元素。

**初始化：** 每个元素都位于一个单独的树，表示为一棵只有根节点的树。将根节点的父亲设为自己。

```cpp
struct dsu {
    vector<int> pa;
    explicit dsu(int size) { 
        pa.resize(size);
        for (int i = 0; i < size; i++) pa[i] = i;
    }
};
```

**查询：** 查询两个元素对应的树的根节点是否相同。

```cpp
int find(int x){
    if (pa[x] == x) {
        return x;
    }
    else {
        return find(pa[x]);
    }
}
```

**（优化）路径压缩：** 在查询根节点的同时，可以将下方的子节点挂到父亲上，以此压缩树的高度，便于之后的查询。

```cpp
int find(int x){
    if (pa[x] == x) {
        return x;
    }
    else {
        pa[x] = find(pa[x]);
        return pa[x];
    }
}
```

**合并：** 合并两个元素对应的树的根，也就是将一个根的父亲设为另一个。

```cpp
void merge(int x, int y){
    pa[find(x)] = find(y);
}
```

**（优化）按秩合并：** 在合并两棵树的时候，我们总是可以将树高更小的树挂在树高更大的树的下方，以此控制树的高度。

```cpp
vector<int> pa;
vector<int> rnk;

explicit dsu(int size) { 
    pa.resize(size);
    rnk.resize(size);
    for (int i = 0; i < size; i++) {
        pa[i] = i;
        rnk[i] = 1;
    }
}

void merge(int x, int y){
    int root_x = find(x);
    int root_y = find(y);
    if (rnk[root_x] > rnk[root_y]) swap(root_x, root_y);
    else if (rnk[root_x] == rnk[root_y]) rnk[root_y]++;
    pa[root_x] = root_y;
}
```

### 例题：【模板】并查集

> **题目链接**：[Luogu P3367](https://www.luogu.com.cn/problem/P3367)
>
> **题目背景**
>
> 本题数据范围已经更新到 $1\le N\le 2\times 10^5$，$1\le M\le 10^6$。
>
> **题目描述**
>
> 如题，现在有一个并查集，你需要完成合并和查询操作。
>
> **输入格式**
>
> 第一行包含两个整数 $N,M$，表示共有 $N$ 个元素和 $M$ 个操作。
>
> 接下来 $M$ 行，每行包含三个整数 $Z_i,X_i,Y_i$。
>
> 当 $Z_i=1$ 时，将 $X_i$ 与 $Y_i$ 所在的集合合并。
>
> 当 $Z_i=2$ 时，输出 $X_i$ 与 $Y_i$ 是否在同一集合内，是的输出 `Y`；否则输出 `N`。
>
> **输出格式**
>
> 对于每一个 $Z_i=2$ 的操作，都有一行输出，每行包含一个大写字母，为 `Y` 或者 `N`。
>
> **数据范围**
>
> - 对于 $15\%$ 的数据，$N \le 10$，$M \le 20$；
> - 对于 $35\%$ 的数据，$N \le 100$，$M \le 10^3$；
> - 对于 $50\%$ 的数据，$1\le N \le 10^4$，$1\le M \le 2\times 10^5$；
> - 对于 $100\%$ 的数据，$1\le N\le 2\times 10^5$，$1\le M\le 10^6$，$1 \le X_i, Y_i \le N$，$Z_i \in \{ 1, 2 \}$。
>

#### Code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
const ll MOD = 998244353;

struct dsu
{
    vector<ll> pa;
    vector<ll> rnk;

    explicit dsu(ll size)
    {
        pa.resize(size);
        rnk.resize(size);
        for (ll i = 0; i < size; ++i)
        {
            pa[i] = i;
            rnk[i] = 1;
        }
    }

    ll find(ll x)
    {
        if (pa[x] == x)
        {
            return x;
        }
        else
        {
            pa[x] = find(pa[x]);
            return pa[x];
        }
    }

    void merge(ll x, ll y)
    {
        ll root_x = find(x);
        ll root_y = find(y);
        if (rnk[root_x] > rnk[root_y])
            swap(root_x, root_y);
        else if (rnk[root_x] == rnk[root_y])
            rnk[root_y]++;
        pa[root_x] = root_y;
    }
};

void solve()
{
    ll n, m, x, y, z;
    bool same;
    cin >> n >> m;
    dsu d = dsu(n);
    for (ll i = 0; i < m; ++i)
    {
        cin >> z;
        if (z == 1)
        {
            cin >> x >> y;
            d.merge(x - 1, y - 1);
        }
        else if (z == 2)
        {
            cin >> x >> y;
            same = (d.find(x - 1) == d.find(y - 1));
            if (same)
                cout << "Y" << "\n";
            else
                cout << "N" << "\n";
        }
    }
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

## 7. ST表

### 问题

解决区间上 **可重复贡献问题** 的快速（ $O(1)$ ）查询。（不支持修改操作）

**可重复贡献问题** 是指对于运算 $opt$![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\operatorname{opt}")，满足 $x\ opt\ x\ =\ x$ ，在区间上询问元素 $opt$ 之和的问题。
例如：$max$ ，$gcd$ 就是符合的 $opt$ 。
也就是说使用两段预处理的区间 $opt$ 和，（可能有重复的）覆盖住待查询的区间，他们两个的区间 $opt$ 和就等于待查询的区间的 $opt$ 和。
![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "x\operatorname{opt} x=x")
### 实现

使用 **倍增** 思想，通过 $O(\log N)$ 的预处理一些区间和，使得任意的 $[l_i,\ r_i]$ 都可以被两个预处理区间覆盖。使用大小为 $2^i$ 的一系列区间，使得总存在一个 $i$ ，使得 $[l,\ l+2^i-1]$ 和 $[r-2^i+1,\ r]$ 可以达到覆盖。 通过计算可知：$i=\lfloor {\log _2 (r-l+1)} \rfloor$ 。因此查询只要 $O(1)$ 的时间。

**预处理：** 令 $f(i,j)$ 表示 $[i,\ i+2^j-1]$ 上的最大值。从 $f(i,0)=a_i$ 开始倍增，$f(i,j+1)=max(f(i,j),f(i+2^j,j))$ 。

```cpp
int max_j = floor(log2(n));
vector<vector<int>> f(n, vector<int>(max_j + 1));
for (int i = 0; i < n; ++i) {
    f[i][0] = a[i];
}
for (int j = 0; j < max_j; ++j) {
    for (int i = 0; i <= n - pow(2, j + 1); ++i) {
        f[i][j + 1] = max(f[i][j], f[i + pow(2, j)][j]);
    }
}
```

**查询：** 使用$[l,\ l+2^i-1]$ 和 $[r-2^i+1,\ r]$ 可以达到覆盖，也就是 $max([l,\ r])=max(f(l,i),\ f(r-2^i+1,i))$ 。其中 $i=\lfloor {\log _2 (r-l+1)} \rfloor$ 。

```cpp
int query(int l, int r){
    cover = floor(log2(r - l + 1));
    return max(f[l - 1][cover], f[r - pow(2, cover)][cover]);
}
```

### 例题：【模板】ST 表 & RMQ 问题

> **题目链接**：[Luogu P3865](https://www.luogu.com.cn/problem/P3865)
>
> **题目描述**
>
> 给定一个长度为 $N$ 的数列，和 $M$ 次询问，求出每一次询问的区间内数字的最大值。
>
> **输入格式**
>
> 第一行包含两个整数 $N,M$，分别表示数列的长度和询问的个数。
>
> 第二行包含 $N$ 个整数（记为 $a_i$），依次表示数列的第 $i$ 项。
>
> 接下来 $M$ 行，每行包含两个整数 $l_i,r_i$，表示查询的区间为 $[l_i,r_i]$。
>
> **输出格式**
>
> 输出包含 $M$ 行，每行一个整数，依次表示每一次询问的结果。
>
> **数据范围**
>
> - 对于 $30\%$ 的数据，满足 $1\le N,M\le 10$；
> - 对于 $70\%$ 的数据，满足 $1\le N,M\le {10}^5$；
> - 对于 $100\%$ 的数据，满足 $1\le N\le {10}^5$，$1\le M\le 2\times{10}^6$，$a_i\in[0,{10}^9]$，$1\le l_i\le r_i\le N$。
>

#### Code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
const ll MOD = 998244353;

void solve() {
    ll n, m;
    cin >> n >> m;
    vector<ll> a(n);
    for (ll i = 0; i < n; ++i) {
        cin >> a[i];
    }
    
    ll max_j = floor(log2(n));
    vector<vector<ll>> f(n, vector<ll>(max_j + 1));
    for (ll i = 0; i < n; ++i) {
        f[i][0] = a[i];
    }
    for (ll j = 0; j < max_j; ++j) {
        for (ll i = 0; i <= n - pow(2, j + 1); ++i) {
            f[i][j + 1] = max(f[i][j], f[i + pow(2, j)][j]);
        }
    }
    
    ll l, r, ans, cover;
    for (ll i = 0; i < m; ++i) {
        cin >> l >> r;
        cover = floor(log2(r - l + 1));
        ans = max(f[l - 1][cover], f[r - pow(2, cover)][cover]);
        cout << ans << "\n";
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

## 8. 线段树

### 问题

解决区间上 **可结合问题** 的 $O(\log N)$ 修改，查询。
相比于**数组** 的 $O(1)$ 修改， $O(N)$ 查询；**前缀和** 的 $O(N)$ 修改， $O(1)$ 查询。**线段树** 给出了一种折中的快速修改，查询的方式。

**可结合问题** 是指对于运算 $+$，满足结合律 $(a+b)+c=a+(b+c)$ ，且空集对应的数值为 $e$ 是加法的单位元，在区间上修改，询问元素 $+$ 的问题。
例如：$(N,\ +)$ ，$(N,\ \times)$ 就是符合的 $+$ 。
也就是说 $+$ 构成一个幺半群，且使用多段不相交预处理的区间和，覆盖住待查询的区间，他们的区间和就等于待查询的区间的总和。
![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "x\operatorname{opt} x=x")
### 实现

**初始化：** 为了方便，我们将待操作数组 $arr$ 扩充到2的幂次的大小 $N$ ，开一个 $2N$ 大小的数组 $tree$ ，初始化 $lazy$ 数组便于后续应用懒标记的区间修改，递归求出每一段初始区间的区间和。

```cpp
struct seg {
    vector<int> tree;
    vector<int> lazy;
    int N;
    explicit seg(vector<int> arr) {
        N = arr.size();
        tree.resize(2 * N);
        lazy.resize(2 * N);
        fill(lazy.begin(), lazy.end(), 0);
        for (int i = 0; i < N; ++i) {
            tree[i + N] = arr[i];
        }
    }
    
    void build(int cur) {
        if (cur < N) {
            build(2 * cur);
            build(2 * cur + 1);
            tree[cur] = tree[2 * cur] + tree[2 * cur + 1];
        }
    }
};
```

**懒标记：** 考虑到区间修改操作对 $tree$ 中节点改动较大，如果要修改区间波及的所有结点，复杂度显然过高。
我们考虑只更新区间修改中对应的极大区间对应节点，运用懒标记指示该节点的后代节点还欠完成一个 $lazy[cur]$ 大小的更改，而对其后代的修改则推迟到后续对其查询或修改的时候再进行。
我们定义一个 $push$ 函数表示在后续过程中需要将 $cur$ 节点的懒标记下推到子节点后对子节点的区间和加回欠的 $lazy[cur]$ 。

```cpp
void push(int cur, int l, int r) {
    if (cur < N and lazy[cur] != 0) {
        int amount = (r - l + 1) / 2 * lazy[cur];
        tree[2 * cur] += amount;
        tree[2 * cur + 1] += amount;
        lazy[2 * cur] += lazy[cur];
        lazy[2 * cur + 1] += lazy[cur];
        lazy[cur] = 0;
    }
}
```

**区间修改：** 我们从1号节点开始向下递归查找所需要的极大子区间们，以此将所需修改的区间拆为若干个子区间的并。在向下递归的过程中，需要同时对路过的点进行 $push$ ，进而更新懒标记，最后当递归到的区间完全被需要修改的区间覆盖时，这就是我们要找的极大子区间，将他们的 $lazy$ 更新即可。

```cpp
void modify(int cur, int l, int r, int ql, int qr, int delta) {
    if (ql <= l and qr >= r) {
        lazy[cur] += delta;
        tree[cur] += delta * (r - l + 1);
    } else {
        int mid = (r + l) / 2;
        push(cur, l, r);
        if (ql <= mid)
            modify(2 * cur, l, mid, ql, qr, delta);
        if (qr > mid)
            modify(2 * cur + 1, mid + 1, r, ql, qr, delta);
        tree[cur] = tree[2 * cur] + tree[2 * cur + 1];
    }
}
```

**区间查询：** 类似进行向下的递归和懒标记的下推，当递归到极大子区间时，将他们的 $tree$ 值加起来即可。

```cpp
int query(int cur, int l, int r, int ql, int qr) {
    if (ql <= l and qr >= r) {
        return tree[cur];
    } else {
        int mid = (r + l) / 2;
        push(cur, l, r);
        int ans = 0;
        if (ql <= mid)
            ans += query(2 * cur, l, mid, ql, qr);
        if (qr > mid)
            ans += query(2 * cur + 1, mid + 1, r, ql, qr);
        return ans;
    }
}
```

### 例题：【模板】线段树 1

> **题目链接**：[Luogu P3372](https://www.luogu.com.cn/problem/P3372)
>
> **题目描述**
>
> 如题，已知一个数列 $\{a_i\}$，你需要进行下面两种操作：
>
> 1. 将某区间每一个数加上 $k$。
> 2. 求出某区间每一个数的和。
>
> **输入格式**
>
> 第一行包含两个整数 $n, m$，分别表示该数列数字的个数和操作的总个数。
>
> 第二行包含 $n$ 个用空格分隔的整数 $a_i$，其中第 $i$ 个数字表示数列第 $i$ 项的初始值。
>
> 接下来 $m$ 行每行包含 $3$ 或 $4$ 个整数，表示一个操作，具体如下：
>
> 1. `1 x y k`：将区间 $[x, y]$ 内每个数加上 $k$。
> 2. `2 x y`：输出区间 $[x, y]$ 内每个数的和。
>
> **输出格式**
>
> 输出包含若干行整数，即为所有操作 2 的结果。
>
> **数据范围**
>
> - 对于 $15\%$ 的数据：$n \le 8$，$m \le 10$。
> - 对于 $35\%$ 的数据：$n \le {10}^3$，$m \le {10}^4$。
> - 对于 $100\%$ 的数据：$1 \le n, m \le {10}^5$，$a_i,k$ 为正数，且任意时刻数列的和不超过 $2\times 10^{18}$。
>

#### Code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
const ll MOD = 998244353;

struct seg {
    vector<ll> tree;
    vector<ll> lazy;
    ll N;
    explicit seg(vector<ll> arr) {
        N = arr.size();
        tree.resize(2 * N);
        lazy.resize(2 * N);
        fill(lazy.begin(), lazy.end(), 0);
        for (ll i = 0; i < N; ++i) {
            tree[i + N] = arr[i];
        }
    }

    void build(ll cur) {
        if (cur < N) {
            build(2 * cur);
            build(2 * cur + 1);
            tree[cur] = tree[2 * cur] + tree[2 * cur + 1];
        }
    }

    void push(ll cur, ll l, ll r) {
        if (cur < N and lazy[cur] != 0) {
            ll amount = (r - l + 1) / 2 * lazy[cur];
            tree[2 * cur] += amount;
            tree[2 * cur + 1] += amount;
            lazy[2 * cur] += lazy[cur];
            lazy[2 * cur + 1] += lazy[cur];
            lazy[cur] = 0;
        }
    }

    void modify(ll cur, ll l, ll r, ll ql, ll qr, ll delta) {
        if (ql <= l and qr >= r) {
            lazy[cur] += delta;
            tree[cur] += delta * (r - l + 1);
        } else {
            ll mid = (r + l) / 2;
            push(cur, l, r);
            if (ql <= mid)
                modify(2 * cur, l, mid, ql, qr, delta);
            if (qr > mid)
                modify(2 * cur + 1, mid + 1, r, ql, qr, delta);
            tree[cur] = tree[2 * cur] + tree[2 * cur + 1];
        }
    }

    ll query(ll cur, ll l, ll r, ll ql, ll qr) {
        if (ql <= l and qr >= r) {
            return tree[cur];
        } else {
            ll mid = (r + l) / 2;
            push(cur, l, r);
            ll ans = 0;
            if (ql <= mid)
                ans += query(2 * cur, l, mid, ql, qr);
            if (qr > mid)
                ans += query(2 * cur + 1, mid + 1, r, ql, qr);
            return ans;
        }
    }
};

void solve() {
    ll n, m, x, y, z, k;
    cin >> n >> m;
    ll upper = pow(2, ceil(log2(n)));
    vector<ll> a(upper, 0);
    for (ll i = 0; i < n; ++i)
        cin >> a[i];

    seg s = seg(a);
    s.build(1);

    for (ll i = 0; i < m; ++i) {
        cin >> z;
        if (z == 1) {
            cin >> x >> y >> k;
            s.modify(1, 1, upper, x, y, k);
        } else if (z == 2) {
            cin >> x >> y;
            cout << s.query(1, 1, upper, x, y) << "\n";
        }
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    solve();
    return 0;
}
```

### 例题：【模板】线段树 2

> **题目链接**：[Luogu P3373](https://www.luogu.com.cn/problem/P3373)
>
> **题目描述**
>
> 如题，已知一个数列 $a$，你需要进行下面三种操作：
>
> - 将某区间每一个数乘上 $x$；
> - 将某区间每一个数加上 $x$；
> - 求出某区间每一个数的和。
>
> **输入格式**
>
> 第一行包含三个整数 $n,q,m$，分别表示该数列数字的个数、操作的总个数和模数。
>
> 第二行包含 $n$ 个用空格分隔的整数，其中第 $i$ 个数字表示数列第 $i$ 项的初始值 $a_i$。
>
> 接下来 $q$ 行每行包含若干个整数，表示一个操作，具体如下：
>
> 操作 $1$：格式：`1 x y k`，含义：将区间 $[x,y]$ 内每个数乘上 $k$。
>
> 操作 $2$：格式：`2 x y k`，含义：将区间 $[x,y]$ 内每个数加上 $k$。
>
> 操作 $3$：格式：`3 x y`，含义：输出区间 $[x,y]$ 内每个数的和对 $m$ 取模所得的结果。
>
> **输出格式**
>
> 输出包含若干行整数，即为所有操作 $3$ 的结果。
>
> **数据范围**
>
> - 对于 $30\%$ 的数据：$n \le 8$，$q \le 10$；
> - 对于 $70\%$ 的数据：$n \le 10^3$，$q \le 10^4$；
> - 对于 $100\%$ 的数据：$1 \le n \le 10^5$，$1 \le q \le 10^5$，$1\le a_i,k\le 10^4$。
>
> 除样例外，$m = 571373$。
>

#### Solution
//

#### Code

```cpp

```