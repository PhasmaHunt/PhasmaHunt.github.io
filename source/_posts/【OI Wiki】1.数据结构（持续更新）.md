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

# 3. 哈希表

### 实现