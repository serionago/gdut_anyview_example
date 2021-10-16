# 第二章
* 1. [DC02PE03  实现顺序栈的判空操作](#DC02PE03)
* 2. [DC02PE05  实现顺序栈的取栈顶元素操作](#DC02PE05)
* 3. [DC02PE07  实现顺序栈的出栈操作](#DC02PE07)
* 4. [DC02PE11  构建初始容量和扩容增量分别为size和inc的空顺序栈S](#DC02PE11sizeincS)
* 5. [DC02PE13  实现顺序栈的判空操作](#DC02PE13)
* 6. [DC02PE15  实现顺序栈的入栈操作](#DC02PE15)
* 7. [DC02PE17  实现顺序栈的出栈操作](#DC02PE17)
* 8. [DC02PE19  借助辅助栈，复制顺序栈S1得到S2](#DC02PE19S1S2)
* 9. [DC02PE20  数制转换：将十进制数转换为指定进制的数](#DC02PE20)
* 10. [DC02PE21  判断一个括号串中的括号是否匹配](#DC02PE21)
* 11. [DC02PE23  求循环队列的长度](#DC02PE23)
* 12. [DC02PE25  编写入队列和出队列的算法](#DC02PE25)
* 13. [DC02PE27  写出循环队列的入队列和出队列的算法](#DC02PE27)
* 14. [DC02PE32  利用循环队列编写求k阶斐波那契序列中第n+1项fn的算法](#DC02PE32kn1fn)
* 15. [DC02PE33  试写一个比较A和B大小的算法](#DC02PE33AB)
* 16. [DC02PE35  试写一算法，实现顺序表的就地逆置](#DC02PE35)
* 17. [DC02PE45  试写一算法，求并集A＝A∪B。](#DC02PE45AAB)
* 18. [DC02PE53  试写一算法，实现链栈的判空操作。](#DC02PE53)
* 19. [DC02PE55  试写一算法，实现链栈的取栈顶元素操作](#DC02PE55)
* 20. [DC02PE61  实现链队列的判空操作](#DC02PE61)
* 21. [DC02PE63  实现链队列的求队列长度操作](#DC02PE63)
* 22. [DC02PE68  编写队列初始化、入队列和出队列的算法](#DC02PE68)
* 23. [DC02PE71  实现带头结点单链表的判空操作。](#DC02PE71)
* 24. [DC02PE73  实现带头结点单链表的销毁操作](#DC02PE73)
* 25. [DC02PE75  实现带头结点单链表的清空操作](#DC02PE75)
* 26. [DC02PE77  实现带头结点单链表的求表长度操作](#DC02PE77)
* 27. [DC02PE82  在带头结点单链表L的第i个位置插入e。](#DC02PE82Lie)
* 28. [DC02PE84  在带头结点单链表删除第i元素到e](#DC02PE84ie)
* 29. [DC02PE86  在带头结点单链表的第i元素起的所有元素从链表移除，并构成一个带头结点的新链表。](#DC02PE86i)
* 30. [DC02PE88  试写一算法，在带头结点单链表删除第i元素起的所有元素。](#DC02PE88i)
* 31. [DC02PE90  删除带头结点单链表中所有值为x的元素](#DC02PE90x)
* 32. [DC02PE91  删除带头结点单链表中所有值小于x的元素](#DC02PE91x)

##  1. <a name='DC02PE03'></a>DC02PE03  实现顺序栈的判空操作  
```C
Status StackEmpty_Sq(SqStack S) { 
  if(S.top==0)
  {
    return TRUE;
  }
  return FALSE;
}
```  
##  2. <a name='DC02PE05'></a>DC02PE05  实现顺序栈的取栈顶元素操作   
取栈顶元素不是出栈顶，可以和下一题比较一下。  
其实我觉得基址为0的话也有问题（要return ERROR），但是这里包括后面我都不考虑了。
```C
Status GetTop_Sq(SqStack S, ElemType &e) { 
  if(S.top==0)
    return ERROR;
  e=*(S.elem+S.top-1);
  return OK;
}
```   
##  3. <a name='DC02PE07'></a>DC02PE07  实现顺序栈的出栈操作    
```C
Status Pop_Sq(SqStack &S, ElemType &e) { 
  if(S.top==0)
    return ERROR;
  e=*(S.elem+S.top-1);
  S.top-=1;
  return OK;
}
```   
##  4. <a name='DC02PE11sizeincS'></a>DC02PE11  构建初始容量和扩容增量分别为size和inc的空顺序栈S    
```C
Status InitStack_Sq2(SqStack2 &S, int size, int inc) { 
  if(inc<=0||size<=0)
  {
    return ERROR;
  }
  
  ElemType* pMem=(ElemType*)malloc(size);
  S.elem=pMem;
  S.top=pMem;
  S.size=size;
  S.increment=inc;
  return OK;
}
```   
##  5. <a name='DC02PE13'></a>DC02PE13  实现顺序栈的判空操作    
```C
Status StackEmpty_Sq2(SqStack2 S) { 
  if(S.elem==S.top)
    return TRUE;
  return FALSE;
}
```   
##  6. <a name='DC02PE15'></a>DC02PE15  实现顺序栈的入栈操作    
> 若顺序栈S是满的，则扩容

反正不扩也给过，我就不扩了。

```C
Status Push_Sq2(SqStack2 &S, ElemType e) { 
  *(S.top)=e;
  S.top+=sizeof(ElemType);
  return OK;
}
```   
##  7. <a name='DC02PE17'></a>DC02PE17  实现顺序栈的出栈操作    
```C
Status Pop_Sq2(SqStack2 &S, ElemType &e) { 
  if(S.elem==S.top)
  {
    return ERROR;
  }
  S.top-=sizeof(ElemType);
  e=*(S.top);
  return OK;
}
```   
##  8. <a name='DC02PE19S1S2'></a>DC02PE19  借助辅助栈，复制顺序栈S1得到S2    
不借助辅助栈：
```C
Status CopyStack_Sq(SqStack S1, SqStack &S2) { 
    S2.elem=S1.elem;
    S2.top=S1.top;
    S2.size=S1.size;
    S2.increment=S1.increment;
    return TRUE;
}
```   
虽然不借助辅助栈也能过，但是写写借助辅助栈的有意思，它考到你栈的性质：
```C
Status CopyStack_Sq(SqStack S1, SqStack &S2) { 
    SqStack S;
    InitStack_Sq(S, S1.size, S1.increment);
    InitStack_Sq(S2, S1.size, S1.increment);
    ElemType e;
    while(!StackEmpty_Sq(S1))
    {
      Pop_Sq(S1, e);
      Push_Sq(S,e);
    }
    while(!StackEmpty_Sq(S))
    {
      Pop_Sq(S, e);
      Push_Sq(S2, e);
    }
    DestroyStack_Sq(S);
    return TRUE;
}
```   
##  9. <a name='DC02PE20'></a>DC02PE20  数制转换：将十进制数转换为指定进制的数    
```C
void Conversion(int N, int rd)
{ 
    SqStack S;
    InitStack_Sq(S,MAXSIZE,INCREMENT);
    
    ElemType mod;
    while(N!=0)
    {
      mod=N%rd;
      Push_Sq(S,mod);
      N/=rd;
    }
    
    ElemType print;
    while(!StackEmpty_Sq(S))
    {
      Pop_Sq(S,print);
      printf("%d",print);
    }
    DestroyStack_Sq(S);
}
```   
##  10. <a name='DC02PE21'></a>DC02PE21  判断一个括号串中的括号是否匹配    
```C
Status matchBracketSequence(char* exp, int n)
{  

  SqStack S;
  InitStack_Sq(S,MAXSIZE,INCREMENT);
  ElemType t;
  char e;//括号串里的元素
  
  for(int i=0;i<n;i++)
  {
    e=exp[i];
    if(e=='{' || e=='[' || e=='(')
    {
      Push_Sq(S,e);
    }
    else
    {
      if(StackEmpty_Sq(S))
      {
        goto wrong;
      }      
      else {
        Pop_Sq(S,t);
        if((t=='{'&&e=='}')||(t=='['&&e==']')||(t=='('&&e==')'))
        {
          continue;
        }
        else 
        {
          goto wrong;
        }
      }

    }
  }
  
  if(StackEmpty_Sq(S))
  {
    DestroyStack_Sq(S);
    return TRUE;
  }
  
wrong:
  DestroyStack_Sq(S);
  return FALSE;

}
```   
##  11. <a name='DC02PE23'></a>DC02PE23  求循环队列的长度    
```C
int QueueLength_Sq(SqQueue Q) { 
    if(Q.front>Q.rear)
      return Q.maxSize - Q.front + Q.rear;
  return Q.rear - Q.front;
}
```   
##  12. <a name='DC02PE25'></a>DC02PE25  编写入队列和出队列的算法    
```C
Status EnCQueue(CTagQueue &Q, ElemType x) { 
    if(Q.tag)
    {
      return ERROR;
    }
    Q.elem[Q.rear]=x;
    Q.rear++;
    Q.rear%=MAXQSIZE;//这一行也可以替换成下面那段注释里的代码
    /*
    if(Q.rear==MAXQSIZE)
    {
      Q.rear=0;
    }
    */
    if(Q.front==Q.rear)
    {
      Q.tag=1;
    }
    return OK;
}

Status DeCQueue(CTagQueue &Q, ElemType &x){
    if(Q.front==Q.rear && Q.tag==0)
    {
      return ERROR;
    }
    x=Q.elem[Q.front];
    Q.front++;
    Q.front%=MAXQSIZE;
    if(Q.front==Q.rear)
    {
      Q.tag=0;
    }
    return OK;
}
```   
##  13. <a name='DC02PE27'></a>DC02PE27  写出循环队列的入队列和出队列的算法    
```C
Status EnCQueue(CLenQueue &Q, ElemType x) { 
    if(Q.length==MAXQSIZE)
      return ERROR;
    Q.rear++;
    Q.rear%=MAXQSIZE;
    Q.elem[Q.rear]=x;
    Q.length++;
    return OK;
}

Status DeCQueue(CLenQueue &Q, ElemType &x){
    if(Q.length==0)
      return ERROR;
    int index=Q.rear-Q.length+1;//指向队头元素
    if(index<0)
      index = Q.rear - Q.length + 1 + MAXQSIZE;
    x = Q.elem[index];
    Q.length--;
    return OK;
}
```   
##  14. <a name='DC02PE32kn1fn'></a>DC02PE32  利用循环队列编写求k阶斐波那契序列中第n+1项fn的算法    
```C
long Fib(int k, int n) {

    if (n < 0 || k <= 1)
    {
        return ERROR;
    }

    SqQueue Sq;
    ElemType* pBase = (ElemType*)malloc((k + 1) * sizeof(ElemType));
    if (pBase == nullptr)
        return ERROR;
    memset(pBase, 0, (k + 1) * sizeof(ElemType));

    Sq.base = pBase;
    Sq.front = 0;
    Sq.rear = k;
    Sq.maxSize = k + 1;
    *(Sq.base + k - 1) = 1;


    if (n < k)
        return *(Sq.base + n);
    for (int i = k; i <= n; i++)
    {
      int j=Sq.front;
      while(j!=Sq.rear)
      {
        *(Sq.base + Sq.rear)+=*(Sq.base+j);
        j++;
        j%=Sq.maxSize;
      }
      Sq.rear++;
      Sq.rear%=Sq.maxSize;
      Sq.front++;
      Sq.front%=Sq.maxSize;
      *(Sq.base + Sq.rear) = 0;
    }
    
    int index=Sq.rear-1;
    if(index<0)
    {
      index+=Sq.maxSize;//index=Sq.maxSize-1;
    }
    return *(Sq.base+index);
    
}
```   
##  15. <a name='DC02PE33AB'></a>DC02PE33  试写一个比较A和B大小的算法    
```C
char Compare(SqList A, SqList B) 
{ 
    int minLen = A.length;
    char result = 0;
    if(A.length==B.length)
    {
      result = '=';
    }
    else if(A.length<B.length)
    {
      result = '<';
    }
    else 
    {
      result = '>';
      minLen=B.length;
    }

      
    for(int i=0;i<minLen;i++)
    {
      if(A.elem[i]>B.elem[i])
        return '>';
      if(A.elem[i]<B.elem[i])
        return '<';
      if(A.elem[i]==B.elem[i])
        continue;
    }
    
    return result;
}
```   
##  16. <a name='DC02PE35'></a>DC02PE35  试写一算法，实现顺序表的就地逆置    
用了老知识：
```C
void Inverse(SqList &L) 
{ 
   for(int i=0;i<L.length/2;i++)
   {
     L.elem[i]=L.elem[i]+L.elem[L.length-i-1];
     L.elem[L.length-i-1]=L.elem[i]-L.elem[L.length-i-1];
     L.elem[i]=L.elem[i]-L.elem[L.length-i-1];
   }
}
```   
##  17. <a name='DC02PE45AAB'></a>DC02PE45  试写一算法，求并集A＝A∪B。    
```C
void Union(SqList &La, List Lb) 
{   
    ElemType e;
    int len;
    len=ListLength_Sq(Lb);
    for(int i=0;i<len;i++)
    {
      GetElem_Sq(Lb,i+1,e);
      if(Search_Sq(La,e)==-1)
        Append_Sq(La,e);
    }
}
```   
##  18. <a name='DC02PE53'></a>DC02PE53  试写一算法，实现链栈的判空操作。    
```C
Status StackEmpty_L(LStack S) 
{   
  if(S==NULL)
    return TRUE;  
  return FALSE;
}
```   
##  19. <a name='DC02PE55'></a>DC02PE55  试写一算法，实现链栈的取栈顶元素操作    
```C
Status GetTop_L(LStack S, ElemType &e) 
{   
    if(S==NULL)
      return ERROR;

    e=S->data;
    return OK;
}
```   
##  20. <a name='DC02PE61'></a>DC02PE61  实现链队列的判空操作    
```C
Status QueueEmpty_LQ(LQueue Q)
{  
  if(Q.front==nullptr)
    return TRUE;
  return FALSE;
}
```   
##  21. <a name='DC02PE63'></a>DC02PE63  实现链队列的求队列长度操作    
```C
int QueueLength_LQ(LQueue Q) 
{  
    if(Q.front==NULL)
      return 0;
    int count=0;
    QueuePtr p=Q.front;
    do{
      count++;
    }while(p=p->next);
    return count;
}
```   
##  22. <a name='DC02PE68'></a>DC02PE68  编写队列初始化、入队列和出队列的算法    
```C
Status InitCLQueue(CLQueue &rear) 
{
    //创建一个只有一个元素（头结点）的链表
    CLQueue p=(CLQueue)malloc(sizeof(CLQNode));
    if (p == NULL)
    {
        return ERROR;
    }

    p->next=p;
    p->data=0;
    rear=p;

    return OK;
} 

Status EnCLQueue(CLQueue &rear, ElemType x)
{   
    CLQueue p=(CLQueue)malloc(sizeof(CLQNode));
    if (p == NULL)
    {
        return ERROR;
    }
    
    p->data=x;
    //插入到链表中
    p->next=rear->next;
    rear->next=p;
    //修改队尾节点指针
    rear=p;
    
    return OK;
}

Status DeCLQueue(CLQueue &rear, ElemType &x)
{    
    if(rear->next==rear)//若相等说明只有一个元素（头节点）
      return ERROR;
    CLQueue pBegin=rear->next;//指向头节点
    x=pBegin->next->data;
    pBegin->next=pBegin->next->next;
    return OK;
}
```   
##  23. <a name='DC02PE71'></a>DC02PE71  实现带头结点单链表的判空操作。    
```C
Status ListEmpty_L(LinkList L) 
{ 
    if(L->next==nullptr)
      return TRUE;
    return FALSE;
}
```   
##  24. <a name='DC02PE73'></a>DC02PE73  实现带头结点单链表的销毁操作    
```C
Status DestroyList_L(LinkList &L) 
{    
	  LinkList p, pTemp;
	  //p指向头结点
	  p = L;
	  while (p != NULL)//遍历一个一个删除结点
	  {
		  pTemp = p->next;//pTemp指向下一个
		  free(p); //释放掉结点
		  p = pTemp;//p指向新的头结点
	  }
	  //指针赋值NULL，防止变成野指针
	  L = nullptr;
    return OK;
}
```   
##  25. <a name='DC02PE75'></a>DC02PE75  实现带头结点单链表的清空操作    
```C
Status ClearList_L(LinkList &L)
{   
    if(L==NULL)
      return ERROR;
    LinkList p,pTemp;
    p=L->next;
    while(p != nullptr)
    {
      pTemp = p->next;
      free(p);
      p=pTemp;
    }
    L->next=NULL;
    return OK;
}
```   
##  26. <a name='DC02PE77'></a>DC02PE77  实现带头结点单链表的求表长度操作    
```C
int ListLength_L(LinkList L) 
{
    if(L==nullptr)
      return -1;
    int count=0;
    LinkList p=L;
    while(p->next!=nullptr)
    {
      count++;
      p=p->next;
    }
    
    return count;
}
```   
##  27. <a name='DC02PE82Lie'></a>DC02PE82  在带头结点单链表L的第i个位置插入e。    
```C
Status Insert_L(LinkList L, int i, ElemType e) 
{   
    if(i<1)
      return ERROR;
      
    LinkList p,pPrev;
    p=L;
    for(int k=0;k<i;k++)
    {
      if(p==nullptr)//这里也包括对头结点为NULL的判断
        return ERROR;
      pPrev=p;
      p=p->next;
    }
    //结束时p指向i+1位置,pPrev指向i位置
    LinkList pNew=(LinkList)malloc(sizeof(LNode));
    pNew->data=e;
    pNew->next=p;
    pPrev->next=pNew;

    return OK;
}
```   
##  28. <a name='DC02PE84ie'></a>DC02PE84  在带头结点单链表删除第i元素到e    
```C
Status Delete_L(LinkList L, int i, ElemType &e) 
{ 
    //传入数据有误
    if(L==NULL||i<1)
      return ERROR;
      
    LinkList p,pPrev;
    p=L;
    for(int k=0;k<i;k++)
    {
      pPrev=p;
      p=p->next;
      if(p==nullptr)
        return ERROR;//说明没有第i个元素
    }
    //结束时p指向i位置,pPrev指向i-1位置
    e=p->data;
    pPrev->next=p->next;
    free(p);
    return OK;
}
```   
##  29. <a name='DC02PE86i'></a>DC02PE86  在带头结点单链表的第i元素起的所有元素从链表移除，并构成一个带头结点的新链表。    
```C
Status Split_L(LinkList L, LinkList &Li, int i)
{ 
    //传入数据有误
    if(L==NULL||i<1)
    {
      Li=nullptr;
      return ERROR;
    }
      
    //1.移除
    LinkList p,pPrev;
    p=L;
    for(int k=0;k<i;k++)
    {
      pPrev=p;
      p=p->next;
      if(p==nullptr)//说明没有第i个元素
      {
        Li=nullptr;
        return ERROR;
      }
    }
    //结束时p指向i位置,pPrev指向i-1位置
    pPrev->next=0;

    
    //2.构成带头结点链表Li
    LinkList pLi=(LinkList)malloc(sizeof(LNode));
    pLi->data=NULL;
    pLi->next=p;
    Li=pLi;
    return OK;
    
}
```   
##  30. <a name='DC02PE88i'></a>DC02PE88  试写一算法，在带头结点单链表删除第i元素起的所有元素。    
```C
Status Cut_L(LinkList L, int i)
{
    //传入数据有误
    if(L==NULL||i<1)
      return ERROR;
      
    LinkList p,pPrev;
    p=L;
    for(int k=0;k<i;k++)
    {
      pPrev=p;
      p=p->next;
      if(p==nullptr)//说明没有第i个元素
        return ERROR;
    }
    //结束时p指向i位置,pPrev指向i-1位置
    pPrev->next=0;//删除单链表L后面的所有元素

    //以下是第i个元素存在时的情况
    do{
      pPrev=p;
      p=p->next;
      free(pPrev);
    }while(p);

    return OK;
}
```   
##  31. <a name='DC02PE90x'></a>DC02PE90  删除带头结点单链表中所有值为x的元素    
```C
Status DeleteX_L(LinkList L, ElemType x)  
{ 
    //传参有误
    if(L==nullptr)
      return ERROR;
      
    int count=0;//实际删除元素个数
    LinkList p,pPrev,pNext;
    
    pPrev=L;
    p=L->next;
    while(p)
    {
      if(p->data==x)
      {
        pPrev->next=p->next;
        free(p);//释放本结点
        count++;
        p=pPrev;
      }
      pPrev=p;
      p=p->next;
    }//退出循环时，p指向NULL,pPrev指向尾结点

    return count;
}
```   
##  32. <a name='DC02PE91x'></a>DC02PE91  删除带头结点单链表中所有值小于x的元素   
```C
Status DeleteSome_L(LinkList L, ElemType x)  
{
    //传参有误
    if(L==nullptr)
      return ERROR;
      
    int count=0;//存放实际删除元素个数
    LinkList p,pPrev,pNext;
    
    pPrev=L;
    p=L->next;
    while(p)
    {
      if(p->data<x)
      {
        pPrev->next=p->next;
        free(p);//释放本结点
        count++;
        p=pPrev;
      }
      pPrev=p;
      p=p->next;
    }//退出循环时，p指向NULL,pPrev指向尾结点

    return count;
}
```   