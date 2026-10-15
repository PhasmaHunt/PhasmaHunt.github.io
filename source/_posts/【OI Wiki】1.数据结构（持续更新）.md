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

## 5. # 二叉堆

### 实现

```cpp

```

