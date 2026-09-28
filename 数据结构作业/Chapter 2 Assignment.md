---
tags: [数据结构, 作业, 链表]
aliases: [数据结构第二章作业]
---

# Chapter 2 Assignment（数据结构作业）

> [!abstract] 一句话定位
> 第二章作业（算法题）：单链表的**原地逆置**、两个有序链表**归并**为逆序链表、两个链表**交替合并**，要求复用原结点、不另开辟存储空间。

---

## 四、算法题

### Q1

#### 1.算法思想

先把递增链表 A、B 分别**原地逆置**为递减链表，再同时扫描 A、B，每次比较当前结点，把**较大者尾插**到 C 的末尾；某一表扫描完后，把另一表剩余部分直接接到 C 后面（剩余部分本身已递减）。

- 时间复杂度：$O(m+n)$（逆置与归并各扫描一遍）
- 空间复杂度：$O(1)$（只改指针，C 复用 A 的头结点）

> [!tip] 另一种思路
> 也可以不逆置：同时扫描 A、B，每次取较小者用**头插法**插入 C，得到的 C 自然是递减的，只需扫描一遍。

***

#### 2. 逆置单链表

```cpp
void Reverse(LinkList L){
    LNode *p = L -> next;
    LNode *pre = NULL;
    LNode *q;

    while (p != NULL){
        q = p -> next; //保存后继
        p -> next = pre; //翻转指针
        pre = p;
        p = q;
    }

    L -> next = pre;
}
```

***

#### 3. 合并算法

```cpp
LinkList MergeList(LinkList A, LinkList B)
{
    // 先将 A、B 逆置为递减链表
    Reverse(A);
    Reverse(B);
    LNode *p = A->next;
    LNode *q = B->next;
    LNode *s;

    // 用 A 的头结点作为 C 的头结点
    A->next = NULL;
    LNode *r = A;       // r 指向 C 的尾结点

    while (p != NULL && q != NULL)
    {
        if (p->data >= q->data)
        {
            s = p;
            p = p->next;
        }
        else
        {
            s = q;
            q = q->next;
        }

        // 尾插到 C
        r->next = s;
        r = s;
    }
    // 剩余部分本身已经递减，直接接到 C 后面
    if (p != NULL)
        r->next = p;
    else
        r->next = q;

    delete B;       // B 的头结点不再需要
    return A;       // A 即为新的 C
}
```

### Q2

#### 1. 算法思想

设：

```text
A: a1 -> a2 -> a3 -> ...
B: b1 -> b2 -> b3 -> ...
```

交替取节点：

```text
a1 -> b1 -> a2 -> b2 -> a3 -> b3 ...
```

如果某个链表先结束，就把另一个链表剩余部分直接接到 C 后面。时间复杂度 $O(\min(m,n))$，空间复杂度 $O(1)$。

***

#### 2. 算法代码

```cpp
LinkList Merge(LinkList A, LinkList B)
{
    LNode *p = A->next;    // 扫描 A
    LNode *q = B->next;    // 扫描 B
    LNode *r = A;          // r 指向 C 的尾结点
    LNode *s;
    A->next = NULL;        // 用 A 的头结点作为 C 的头结点

    while (p != NULL && q != NULL)
    {
        // 取 A 的一个结点
        s = p;
        p = p->next;
        r->next = s;
        r = s;
        // 取 B 的一个结点
        s = q;
        q = q->next;
        r->next = s;
        r = s;
    }

    // 把剩余结点直接接上
    if (p != NULL)
        r->next = p;
    else
        r->next = q;

    delete B;              // B 的头结点不用了
    return A;
}
```

---

## 📎 相关笔记

**课程**：[[00 数据结构索引|数据结构]] ｜ **上一篇**：[[Chapter 1 Assignment]]

- [[Lesson 01 数据结构与算法基础]] —— 对应讲义：链式存储结构
