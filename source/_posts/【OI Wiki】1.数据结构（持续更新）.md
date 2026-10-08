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
vector<int> a();
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
deque<int> a();
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

# 2. 链表

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

### 例题：[【模板】双向链表](https://www.luogu.com.cn/problem/B4324)

> **题目描述**
> 给出 $N$ 个结点，编号依次为 $1 \dots N$，初始按编号从小到大排列成一条双向链表。
> 接下来有 $M$ 条指令，请按要求对链表进行修改。所有操作均保证合法。
> 
> | 指令 | 含义 |
> | :--- | :--- |
> | `1 x y` | 将结点 $x$ 插入到 $y$ 的左侧（若 $x=y$ 则忽略本条指令）。 |
> | `2 x y` | 将结点 $x$ 插入到 $y$ 的右侧（若 $x=y$ 则忽略本条指令）。 |
> | `3 x` | 删除结点 $x$；若 $x$ 已被删除则忽略本条指令。 |
> 
> 操作结束后，请按**从左到右**的顺序输出当前链表中所有结点的编号。
> 
> **输入格式**
> 第一行输入两个正整数 $N, M$，表示链表初始的结点数和操作指令数。
> 接下来 $M$ 行，每行一条指令，如题意所述。
> 
> **输出格式**
> 输出一行，即：操作结束后，按从左到右的顺序输出当前链表中所有结点的编号。如果链表不存在结点，输出 `Empty!`。
> 
> **数据范围**
> 对于 $30\%$ 的数据，$1 \le N, M \le 10$；
> 对于 $60\%$ 的数据，$1 \le N, M \le 3000$；
> 对于所有数据，$1 \le N, M \le 5 \times 10^5$。
