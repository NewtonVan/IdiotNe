---
title: Data Structure
date: 2019-08-31 17:36:38
tags: Base
categories: Programming
mathjax: true
---

# Overview
***

This is the reading note about the 3 books of data structure. More specifically, the main idea is from the *Data structures and Algorithm Analysis in C* and the other 2 books of TsingHua Univesity consists of the supplementary or regeneralize some operation in the*Data structures and Algorithm Analysis in C* in another way. And I will add more details about these data structures in the other blogs.

This is just a blog about some basic data structure. I'll write a blog about the advance data structure in other blogs.

# List, Stack and Queue
***

## Linked List
***

To reduce the cost of deletion  and insertion, we avoid storing the data sequentially. Linked list is the data structure that achieve this goal. Linded list consist of the memory cells that doesn't need to be adjacent in memory.

### Some Preparation For TsingHua's Books
***
```c
#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0
typedef int Status;
```

### Programming details
***

* There is no obvious way to insert at the front of the list from the definitions given.
* Deleting from the front of the list is a special case, because it changes the start of the list.
* Deletion in general.

To solve these three problems, we create a sentinal node called header or dummy node. 

```c
#ifndef _List_H
#define _List_H

struct Node;
typedef struct Node *PtrToNode;
typedef PtrToNode List;
typedef PtrToNode Position;

List MakeEmpty(List L);
int IsEmpty(List L);
int IsLast(Position P, List L);
Position Find(ElementType X, List L);
void Delete(ElementType X, List L);
Position FindPrevious(ElementType X, List L);
void Insert(ElementType P, List L, Position P);
void DeleteList(List L);
Position Header(List L);
Position First(List L);
Position Advance(Position P);
ElementType Retrieve(Position P);

#endif

/*Place in the implementation file*/

struct Node
{
    ElementType Element;
    Position Next;
}
```
The function to test whether the linked list is empty.
```c
/*Return true if the list is empty*/
int IsEmpty(List L)
{
    return NULL == L->Next;
}
```

Test whether the current position is the end of the list.
```c
/*Return true if P is the last position in list L*/
/*Parameter is unused in this implementation*/

int IsLast(Position P, List L)
{
    return NULL == P->Next;
}
```

We must avoid use recursion to achieve Find.
```c
/*Return Position of X in L; NULL if not find*/
Position Find(ElementType X, List L)
{
    Position P;

    P = L->Next;
    while (NULL != P && X != P->Element){
        P = P->Next;
    }

    return P;
}
```

Our fourth routine is to delete the first occurance of X from L. Addtionally, we will also achieve the function FindPrevious.
```c
/*Delete first occurance of X from a list */
/*Assume use of a header node*/

void Delete(ElementType X, List L)
{
    Position P, TmpCell;
    P = FindPrevious(P, L);

    if (!IsLast(P, L)){
        TmpCell = P->Next;
        P->Next = TmpCell->Next;
        free(TmpCell);
    }
}

Position FindPrevious(ElementType X, List L)
{
    Position P;
    P = L;

    while (NULL != P->Next && X != P->Next->Element){
        P = P->Next;
    }

    return P;
}
```

```c
/*Insert (after legal position P)*/
/*Header implementation assumed*/
/*Parameter L is unused in this implementation*/

void Insert(ElementType X, List L, Position P)
{
    Position TmpCell;

    TmpCell = (Position)malloc(sizeof(struct Node));
    if (NULL == TmpCell){
        FatalError("Out of  space!!!");
    }

    TmpCell->Element = X;
    TmpCell->Next = P->Next;
    P->Next = TmpCell;
}
```
### Supplementary About the Programming details of Linked List
***

```c
/*Function GetElem is used to get the ith node's data*/
/* Use e to return the result of the ith data*/
Status GetElem(List L, int i, ElementType &e)
{
    int j;
    List T;
    T = L->Next;
    j = 1;

    while (T && j<i){
        T = T->Next;
        ++j;
    }
    if (!T || j>i){
        return ERROR;
    }

    e = T->Element;
    return OK;
}
/*Another way to insert the new data e*/
// ListInsert will insert the new node e before the ith node.
Status ListInsert(List *L, int i, ElementType e)
{
    int j = 1;
    List T, S;
    T = *L;

    while ( T && j<i){
        T = T->Next;
        ++j;
    }

    if (!T || j>i){
        return ERROR;
    }

    S = (List)malloc(sizeof(Node));
    S->Element = e;
    S->Next = T->Next;
    T->Next = S;

    return OK;
}

/*Another way to delete the data*/
/*Delete ith node*/
Status ListDelete(List *L, int i, ElementType &e)
{
    int j = 1;
    List T, S;
    T = *L;

    while (T->Next && j<i){
        T = T->Next;
        ++j;   
    }

    if (!(T->Next) || j>i){
        return ERROR;
    }

    S = T->Next;
    T->Next = S->Next;
    e = S->Element;
    free(S);

    return OK;
}

/*Create a List with header Node.*/
void CreateListHead(List *L, int n)
{
    List T;
    int i;
    srand(time(0));
    *L = (List)malloc(sizeof(Node));
    (*L)->Next = NULL;

    for (i = 0; i<n; i++){
        T = (List)malloc(sizeof(Node));
        T->Element = rand()%100+1;
        T->Next = (*L)->Next;
        (*L)->Next = T;
    }
}

void CreateListTail(List *L, int n)
{
    List T, S;
    int i;
    srand(time(0));
    *L = (List)malloc(sizeof(Node));
    T = *L;

    for (i = 0; i<n; i++){
        S = (List)malloc(sizeof(Node));
        S->Element= rand()%100+1;
        T->Next = S;
        T= S;
    }

    T->Next= NULL;
}

/*Merge to Linked List*/
void MergeList(List &La, List &Lb, List &Lc)
{
    List Pa, Pb, Pc;
    Pa= La->Next;
    Pb= Lb->Next;
    Lc= Pc= La;

    while (Pa && Pb){
        if (Pa->Element <= Pb->Element){
            Pc->Next = Pa;
            Pc= Pa;
            Pa= Pa->Next;
        }
        else{
            Pc->Next= Pb;
            Pc= Pb;
            Pb= Pb->Next;
        }
    }
    Pc->Next= Pa?Pa:Pb;
    free(Lb);
}

/* Delete the whole list*/
Status ClearList(List *L)
{
    List T, S;
    T = (*L)->Next;

    while (T){
        S = T->Next;
        free(T);
        T = S;
    }

    (*L)->Next = NULL;

    return OK;
}
```

And these two books also recommend the static linked list. Attention, the first element of the static linked list store the position of the first element of the back up Linked List, and the last element store the position of the first data point that is inserted.

```c 
#define MAXSIZE 10000000
typedef struct 
{
    ElementType Element;
    int cur;  // cur is the same as the Next pointer in the Node
}Component, StaticLinkedList[MAXSIZE];

Status InitList(StaticLinkedList space)
{
    int i;
    for (i = 0; i<MAXSIZE-1; ++i){
        space[i].cur = i+1;
    }

    space[MAXSIZE-1].cur = 0;

    return OK;
}

/* achieve the malloc function of ourselves*/
int Malloc_SLL(StaticLinkedList space)
{
    int i = space[0].cur;

    if (space[0].cur){
        space[0].cur = space[i].cur;
    }

    return i;
}

Status ListInsert(StaticLinkedList L, int i, ElementType e)
{
    int j, k, l;
    k = MAXSIZE -1;
    if (i<1 || i>ListLength(L)+1){
        return ERROR;
    }

    j = Malloc_SLL(L);
    if (j){
        L[j].Element = e;
        for (l=1; l<i; ++l){
            k = L[k].cur;
        }
        
        L[j].cur = L[k].cur;
        L[k].cur = j;

        return OK;
    }

    return ERROR;
}

Status ListDelete(StaticLinkedList L, int i)
{
    int j, k;
    if (i<1 || i>ListLength(L)){
        return ERROR;
    }

    k = MAXSIZE - 1;
    for (j= 1; j<i; ++j){
        k = L[k].cur;
    }

    j = L[k].cur;
    L[k].cur = L[j].cur;
    Free_SSL(L, j);

    return OK;
}

void Free_SSL(StaticLinkedList space, int k)
{
    space[k].cur = space[0].cur;
    space[0].cur = k;
}

int ListLength(StaticLinkedList L)
{
    int j = 0;
    int i = L[MAXSIZE-1].cur;

    while (i){
        i = L[i];
        ++j;
    }

    return j;
}
```
### Doubly Linked List
***

It is convenient to traverse the linked list inversly in this way.
```c
typedef struct DulNode
{
    ElementType data;
    struct DulNode *prior;
    struct DulNode *next;
}DulNode, *DuLinkList

```
### Circularly Linked List
***

A popular convention is to have the last cell keep a pointer back to the first. This can be done without a header and can also be done with doubly linked lists.

The main difference between circularly linked list and the plain linked list is the condition of judgement. The condition of circularly linked list is to judge whether Next node equal to header node.

To visit both the head and the rear of the linked list, we change the head pointer to the tail pointer that point to the rear of the linked list. In this way, we can find the header node use rear->Next->Next.

The routine to merge to circularly is simple by using rear pointer.
```c
Status MergeCirCularlyLinkedList(List rearA, List rearB)
{
    List T, S;
    T = rearA->Next;
    rearA->Next = rearB->Next->Next;
    S = rearB->Next;
    rearB->Next = T;

    free(S);

    return OK; 
}
```

### Example: The Polynomial ADT
***

We can define an abstract data type for single-variable polynomials by using a list. However this is only adequate for dense polynomials.

To solve the more general problem, we'd bette use a linked list to represent the polynomial and define some routine to make some operation.

The codes of this part are mainly come from the two books of Tsing Hua.

```c
typedef struct
{
    float coef;
    int expn;
}term, ElementType;

typedef List polynomial;


```

### Example: Radix Sort
***

## Stack ADT
***

### Stack Model
Stack is a data structure that constrain the insertion and deletion at the same place, which is called its top. The corresponding operations of insertion and deletion are called **push** and **pop**. 

Sometimes, stack also called as LIFO list.

### Stack Made By Linked List

```c
#ifndef _Stack_H
#define _Stack_H

struct Node;
typedef Node *PtrToNode;
typedef PtrToNode Stack;

int IsEmpty(Stack S);
Stack CreateStack(void);
void DisposeStack(Stack S);
void MakeEmpty(Stack S);
void Push(ElementType X, Stack S);
ElementType Top(Stack S);
ElementType Pop(Stack S);

#endif

/*Place in implementation file*/
/*Stack implementation is a linked list with a header*/
struct Node
{
    ElementType Element;
    PtrToNode Next;
}

```

Functions definitions:

```c
int IsEmpty(Stack S)
{
    return NULL == S->Next;
}

```

Create a stack and make the stack empty.
```c
Stack CreateStack(void)
{
    Stack S;

    S = (Stack)malloc(sizeof(Node));
    if (NULL == S){
        FatalError("Out of space");
    }

    S->Next = NULL;
    MakeEmpty(S);
    return S;
}

void MakeEmpty(Stack S)
{
    if (NULL == S){
        Error("Make use CreateStack first.");
    }
    else{
        while (!IsEmpty(S)){
            Pop(S);
        }
    }
}
```

Three important operations:

```c
void Push(ElementType X, Stack S)
{
    PtrToNode TmpCell;

    TmpCell = (PtrToNode)malloc(sizeof(Node));

    if (NULL == TmpCell){
        FatalError("Out of space");
    }
    else{
        TmpCell->Element = X;
        TmpCell->Next = S->Next;
        S->Next = TmpCell;
    }
}

ElementType Top(Stack S)
{
   if (!IsEmpty(S)){
        return S->Next->Element;
   }

   Error("Empty Stack");

   return [warning value] //return value  used to avoid warning
}

void Pop(Stack S)
{
    PtrToNode FirstCell;

    if (IsEmpty){
        Error("Empty Stack");
    }
    else{
        FirstCell = S->Next;
        S->Next = FirstCell->Next;
        free(FirstCell);
    }
}
```

### Stack Made By Array
***

```c
#ifndef _Stack_h
#define _Stack_h
struct StackRecord;
typedef struct StackRecord *Stack;

int IsEmpty(Stack S);
int IsFull(Stack S);
Stack CreateStack(int MaxElements);
void DisposeStack(Stack S);
void MakeEmpty(Stack S);
void Push(ElementType X, Stack S);
ElementType Top(Stack S);
void Pop(Stack S);
ElementType PopAndPop(Stack S);

#endif

/*Stack in implementation file is a dynamically allocated array*/
#define EmptyTOS -1
#define MinStackSize [any number]
struct StackRecord
{
    int Capacity;
    int TopOfStack;
    ElementType *Array;
};
```

Create a stack:
```c
Stack CreateStack(int MaxElements)
{
    Stack S;

    if (MaxElements < MinStackSize){
        Error("Stack size is too small");
    }

    S = (Stack)malloc(sizeof(struct StackRecord));
    if (NULL == S){
        FatalError("Out of space");
    }

    S->Array = (ElementType*)malloc(sizeof(Elementype)*MaxElements);
    if (NULL == S->Array){
        FatalError("Out of space");
    }

    S->Capacity = MaxElements;
    MakeEmpty(S);

    return S;
}
```

Dispose the stack:
```c
void DisposeStack(Stack S)
{
    if (NULL != S){
        free(S->Array);
        free(S);
    }
}
```

```c
int IsEmpty(Stack S)
{
    return EmptyTOS== S->TopOfStack;
}

void MakeEmpty(Stack S)
{
    S->TopOfStack= EmptyTOS;
}

void Push(Elementype X, Stack S)
{
    if(IsFull(S)){
        Error("Full Stack");
    }
    else{
        S->Array[++S->TopOfStack]= X;
    }
}

Elementype Top(Stack S)
{
    if (!IsEmpty(S)){
        return S->Array[TopOfStack];
    }

    Error("Empty Stack");
    return 0;
}

void Pop(Stack S)
{
    if (IsEmpty(S)){
        Error("Empty Stack");
    }
    else{
        --S->TopOfStack;
    }
}

Elementype TopAndPop(Stack S)
{
    if (IsEmpty(S)){
        return S->Array[S->TopAndPop--];
    }
    Error("Empty Stack");

    return 0;
}
```

### Application
***

## Queue
***

Queue is an abstract data structure that constrain the insertion at one side of the list and the deletion at the other side. Queue is also called FIFO ADT.

### Queue Made By Array
***

```c
#ifndef _Queue_H
#define _Queue_H

struct QueueRecord;
typedef struct QueueRecord *Queue;

int IsEmpty(Queue Q);
int IsFull(Queue Q);
Queue CreateQueue(int MaxElements);
void DisposeQueue(Queue Q);
void MakeEmpty(Queue Q);
void Enqueue(Elementype X, Queue Q);
ElementType Front(Queue Q);
void Dequeue(Queue Q);
Elementype FrontAndDequeue(Queue);

#endif

/*Place in implementation file*/
/*Queue implementation is a dynamically allocated array*/
#define MinQueueSize [any positive number]

struct QueueRecord
{
    int Capacity;
    int Front;
    int Rear;
    int Size;
    Elementype *Array
};
```

Some routine:

```c
int IsEmpty(Queue Q)
{
    return 0== Q->Size;
}

void MakeEmpty(Queue Q)
{
    Q->Size= 0;
    Q->Front= 1;
    Q->Rear= 0;
}

Static int Succ(int Value, Queue Q)
{
    if (++Value== Q->Capacity){
        Value= 0;
    }

    return Value;
}

void Enqueue(Elementype X, Queue Q)
{
    if (!IsFull(Q)){
        ++Q->Size;
        Q->Rear= Succ(Q->Rear, Q);
        Q->[Q->Rear]= X;
    }    
    else{
        Error("Full Queue");
    }
}
```

### Queue Implemented By Linked List(Supplementary)
***

Some preparations:

```c
typedef struct QNode{
    QElemType data;
    struct QNode *next;

}QNode, *QueuePtr;

typedef struct{
    QueuePtr front;
    QueuePtr rear;
}LinkQueue;
```

Routines:

```c
Status EnQueue(LinkQueue *Q, QElemType e)
{
    QueuePtr s= (QueuePtr)malloc(sizof(QNode));

    if (!s)
        exit(OVERFLOW);
    s->data= e;
    s->next= NULL;
    Q->rear->next= s;

    Q->rear= s;

    return OK;
}

Status Dequeue(LinkQueue *Q, QElemType *e)
{
    QueuePtr p;
    if (Q->front== Q->rear){
        return ERROR;
    }

    p= Q->front->next;
    *e= p->data;
    Q->front->next= p->next;

    if (Q->rear== p){
        Q->rear= Q->front;
    }

    free(p);

    return OK;
}
```

# String
***

This chapter consists of the contents from two Tsing Hua's books.

## Definition
***

**String is an ordered sequence made by none character or many characters.**

We denoted a string *s* as:


$$s= a_{1} a_{2} \cdots a_{n}$$

The number of the characters in the string is called the *length* of the string. If the string doesn't have any character, we call it the *null string*.

## The Comparasion Between Strings
***

$s= "a_{1} a_{2} \cdots a_{n}"$
$t= "a_{1} a_{2} \cdots a_{m}"$

If any condition of the two conditions displayed below is satisfied, we define this $s<t$.

* $n<m$, &$a_i= b_i$.
* There exist some $k\leq min(m, n)$ such that $a_i= b_i(i= 1, 2, \cdots, k-1), a_k<b_k$


## The Storage Structure Of The String
***

It can be divided into two types.

### The Sequential Storage Structure
***

It is a sequence of characters which have a contiguous set of addresses. This kind of strings usually have to ensure the enough space for the string.

### Chain Storage Structure
***

It has a waste of the space and it doesn't flexible like the sequential storage structure.

## Pattern Matching Algorithm(KMP)
***

Actually, I intend to write another blog to focus on some pattern matching algorithm from *Handbook of Exact String Matching Algorithms*.

In this blog, we just simply focus on KMP Pattern Matching Algorithm. More specifically, the C code of KMP.

```c
void PreKMP(char *x, int m, int KmpNext[])
{
    int i, j;

    i= 0;
    j= KmpNext[0]= -1;  // j is always the end index of the prefix substring.

    while (i<m){
        while (j> -1 && x[i]!= x[j]){
            j= KmpNext[j]; 
        }                       
        // To simplify the code, we add the while loop at here
        ++i;
        ++j;
        if (x[i]== x[j]){
            KmpNext[i]= KmpNext[j];
        }
        else
            KmpNext[i]= j;
    }
}
void KMP(char *x, int m, char *y, int n)
{
    int i, j, KmpNext[XSIZE];

    PreKMP(x, m, KmpNext);

    i= j= 0;
    while (j<n){
        while (i>-1 && x[i]!= y[j]){
            i= KmpNext[i];
        }
        ++i;
        ++j;
        if (i>= m){
            OUTPUT(j-i);
            i= KmpNext[i];
        }
    }
}
```
Another C code:
```c
void GetNext(String T, int *next)
```
# Tree 
***

For the big size of the data set, linear time to access is too slow. The tree is a data structure which most of its operation can be implemented in $\Omega(N)$ time.

## Definition
***

In generally, we define a tree data structure by recursion. 

A tree is the set of some nodes. This set can be null. If not, a tree consist of a node r named **root** and lots of subtrees which are not empty. What's more, every root node from these subtrees is linked by a directed edge from the node r.

The amount of the subtrees the node own is defined as the degree of the node. And the node with 0 degree is called as the leaf node. The node of the tree is defined as the maximum degree of the node in the tree. 

The root of the subtree which the node own is called as child. And the node is known as parent. Two child with the same parent are sibling. 

The level is counted from the root. And the maximum level of the tree is called the depth.

Forest is a set of disjoint trees. 

## The Traverse And Application Of The Tree
***



# Hash
***

Hash technique is set up a relation between its key word and its storage location. We call the relation as hash function.

## Process
***

* design hash functions
* use hash functions to store the keyword
* deal with the collision
* search the location by hash functions and the keyword you wanna find
* if there is a collision, solve it

## Principles Of Designing Hash Function
***

* Easy to calculate
* It's distribution is as uniform as possible

## Direct-address Table
***

It is designed for the situation the whole domain U is small. It is convenient for us to use keyword as its index.

We can also use a linear function of its keyword as hash functions.

## Analyze Numbers Method
***

We can extract part of the keyword and do some other operation on this part as its index. This is based on the analysis we have about the data we gonna handle. 



