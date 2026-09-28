# 四、算法题

## Q1
### 1.算法思想

**将原链表逆序排序，使其逆序排序，然后同时扫描A、B，每次比较当前节点，将最大的置于C末尾。**

***
### 2. 逆置单链表

```C++
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
### 3. 合并算法

```C++
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

## Q2

### 1. 算法思想
设：
```TEXT
A: a1 -> a2 -> a3 -> ...
B: b1 -> b2 -> b3 -> ...
```
交替取节点：
```TEXT
a1 -> b1 -> a2 -> b2 -> a3 -> b3 ...
```
如果某个链表先结束，就把另一个链表剩余部分直接接到C后面。

***

### 2. 算法代码

```C++
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