---
sort: 1
---
# 第一章
* 1. [DC01PE06 将三个整数按升序重新排列](#DC01PE06)
* 2. [DC01PE08 求一元多项式的值](#DC01PE08)
* 3. [DC01PE11 求k阶裴波那契序列的第m项的值](#DC01PE11km)
* 4. [DC01PE18 计算i!×2^i的值](#DC01PE18i2i)
* 5. [DC01PE20 按照特定顺序打印“学生”结构体数组中所有学生的姓名](#DC01PE20)
* 6. [DC01PE21 查找学生结构体数组中的最高成绩](#DC01PE21)
* 7. [DC01PE22 打印“学生”结构体数组中第一个最高成绩学生的姓名和成绩](#DC01PE22)
* 8. [DC01PE23 打印“学生”结构体数组中最后一个最高成绩学生的姓名和成绩](#DC01PE23)
* 9. [DC01PE30 将结构体中的字符串逆序放置](#DC01PE30)
* 10. [DC01PE49 由一维数组构建一个序列](#DC01PE49)
* 11. [DC01PE61 构建一个值为x的结点](#DC01PE61x)
* 12. [DC01PE63 构建长度为2且两个结点的值依次为x和y的链表](#DC01PE632xy)
* 13. [DC01PE65 构建长度为2的升序链表](#DC01PE652)

##  1. <a name='DC01PE06'></a>DC01PE06 将三个整数按升序重新排列
```C
// 通过交换，令 a >= b >= c
void Descend(int &a, int &b, int &c)  
{   
  if(a<b)
  {
    a=a+b;
    b=a-b;
    a=a-b;
  }
  if(a<c)
  {
    a=a^c;
    c=a^c;
    a=a^c;
  }
  if(b<c)
  {
    int t;
    t=b;
    b=c;
    c=t;
  }
}
```
##  2. <a name='DC01PE08'></a>DC01PE08 求一元多项式的值
```C
#include <math.h>
float Polynomial(int n, int a[], float x0) 
{   // Add your code here
  float result=0;
  int i=0;
  while(i<=n)
  {
    result+=a[i]*pow(x0,i);
    i++;
  }
  return result;
}
```
##  3. <a name='DC01PE11km'></a>DC01PE11 求k阶裴波那契序列的第m项的值
这个版本能跑，但是不太喜欢：
```C
Status Fibonacci(int k, int m, int &f) { 
    //求k阶第m项值的函数
    //能求得k阶m项的值f，则返回OK,否则ERROR
    //K阶斐波那契数列的前k-1项均为0（0~k-2），第k-1项为1，以后的每一项都是前k项的和
    //化简得迭代公式：
    //①：f(m)=f(m-1)+f(m-2)+…+f(m-k) 
    //②：f(m-1)=f(m-2)+f(m-3)+…+f(m-k-1)              
    //①-②: f(m)-f(m-1)=f(m-1)-f(m-k-1)->f(m)=2f(m-1)-f(m-k-1) 
    if(m<0||k<=1)
    {
      return ERROR;
    }
    
    int a[1000];
    for(int i=0;i<k-1;i++)
    {
      a[i]=0;
    }
    a[k-1]=1;
    a[k]=1;
    if(k>=m)
    {
      f=a[m];
      return OK;
    }
    for(int i=k+1;i<=m;i++)
    {
      a[i]=2*a[i-1]-a[i-k-1];
    }
    f=a[m];
    return OK;
}
```
感觉好一些：
```C
void indexPlus(int &p, int k)
{
    p++;
    p %= k+2;
    return;
}
Status Fibonacci(int k, int m, int &f) { 
    //求k阶第m项值的函数
    //能求得k阶m项的值f，则返回OK,否则ERROR
    //K阶斐波那契数列的前k-1项均为0（0~k-2），第k-1项为1，以后的每一项都是前k项的和
    //若要求下一项，就需要前一项的数值
    if(m<0||k<=1)
    {
      return ERROR;
    }
    
    //一个数组用于保存f(m-k-1)
    //初始化
    int a[k+2]={0};
    a[k-1]=1;//f(k-1)=1
    a[k]=1;//f(k)=1
    int pAgo=0;//索引指针指向f(i-k-1)
    int pPrev=k;//索引指针指向f(i-1)
    int p=k+1;//索引指针指向f(i)
    
    if(m<=k)
    {
      f = a[m];
      return OK;
    }
    //从k+1项开始求，一直求到第m项，然后结束
    for(int i=k+1;i<m+1;i++)
    {
      a[p]=2*a[pPrev]-a[pAgo];
      pPrev=p;
      indexPlus(p,k);
      indexPlus(pAgo,k);
    }
    f = a[pPrev];
    return OK;
}
```
##  4. <a name='DC01PE18i2i'></a>DC01PE18 计算i!×2^i的值
```C
#include <math.h>
Status Series(int a[], int n) { 
  if(n==0)
    return ERROR;
  int mul=1;
  for(int i=1;i<=n;i++)
  {
    mul*=i;
    a[i-1]=mul*pow(2,i);
    if(a[i-1]>MAXINT)
      return EOVERFLOW;
  }
  return OK;
}
```
##  5. <a name='DC01PE20'></a>DC01PE20 按照特定顺序打印“学生”结构体数组中所有学生的姓名
总感觉这里用for循环每个字节的print更保险，但是直接printf也能过。
```C
void printName(stuType student[], int index[], int n)
{  
  for(int i=0;i<n;i++)
  {
    printf("%s\n",student[index[i]].name);
  }
}
```
##  6. <a name='DC01PE21'></a>DC01PE21 查找学生结构体数组中的最高成绩
```C
float highestScore(stuType *student[], int n)
{ 
  float max=0.0;
  for(int i=0;i<n;i++)
  {
    if(student[i]->score>max)
    {
      max=student[i]->score;
    }
  }
  return max;
}
```
##  7. <a name='DC01PE22'></a>DC01PE22 打印“学生”结构体数组中第一个最高成绩学生的姓名和成绩
```C
void printFirstName_HighestScore(stuType *student[], int n)
{  
  char* mName;
  float mMax=0.0;
  for(int i=0;i<n;i++)
  {
    if(mMax<student[i]->score)
    {
      mMax=student[i]->score;
      mName=(char*)&(student[i]->name);
    }
  }
  for(int i=0;i<4;i++)
  {
    printf("%c",mName[i]);
  }
  printf("\n%.2f\n",mMax);
}
```
##  8. <a name='DC01PE23'></a>DC01PE23 打印“学生”结构体数组中最后一个最高成绩学生的姓名和成绩
```C
void printLastName_HighestScore(stuType *student[], int n)
{ 
  char* mName;
  float mMax=0.0;
  for(int i=0;i<n;i++)
  {
    if(mMax<=student[i]->score)
    {
      mMax=student[i]->score;
      mName=(char*)&(student[i]->name);
    }
  }
  for(int i=0;i<4;i++)
  {
    printf("%c",mName[i]);
  }
  printf("\n%.2f\n",mMax);
}
```
##  9. <a name='DC01PE30'></a>DC01PE30 将结构体中的字符串逆序放置
```C
StrSequence* reverseStr(StrSequence* strSeq)
/*返回一个结构体，该结构体将strSeq中的字符串逆序存放*/
{  
  int len=strSeq->length;//取出结构体的字符串长度
  ElemType* pElem=strSeq->elem;//取出结构体的字符串

  ElemType* str=(ElemType*)malloc(len*sizeof(ElemType));
  
  
  StrSequence newSS;
  newSS.elem=str;//返回的结构体的字符串
  newSS.length=len;//返回的结构体的长度
  StrSequence* pnewSS=&newSS;

  for(int i=0;i<len;i++)
  {
    str[i]=*(pElem+len-i-1);
  }
  return pnewSS;
}
```
##  10. <a name='DC01PE49'></a>DC01PE49 由一维数组构建一个序列
```C
Status CreateSequence(Sequence &S, int n, ElemType *a) { 
  if(n<=0)
  {
    return ERROR;
  }
  S.elem=a;
  S.length=n;
  return OK;
}
```
##  11. <a name='DC01PE61x'></a>DC01PE61 构建一个值为x的结点
```C
LinkList MakeNode(ElemType x) { 
  LNode n;
  LinkList pn=&n;
  n.data=x;
  n.next=nullptr;
  return pn;
}
```
##  12. <a name='DC01PE632xy'></a>DC01PE63 构建长度为2且两个结点的值依次为x和y的链表
```C
LinkList CreateLinkList(ElemType x, ElemType y) { 
  int nodeSize=sizeof(ElemType)+sizeof(LinkList);
  LinkList pn1=(LinkList)malloc(nodeSize);
  LinkList pn2=(LinkList)malloc(nodeSize);
  pn1->data=x;
  pn1->next=pn2;
  pn2->data=y;
  pn2->next=nullptr;
  return pn1;
}
```
##  13. <a name='DC01PE652'></a>DC01PE65 构建长度为2的升序链表
```C
LinkList CreateOrdLList(ElemType x, ElemType y) { 
  if(x>y)
  {
    x=x^y;
    y=x^y;
    x=x^y;
  }
  //使x小y大
  int nodeSize=sizeof(ElemType)+sizeof(LinkList);
  LinkList pn1=(LinkList)malloc(nodeSize);
  LinkList pn2=(LinkList)malloc(nodeSize);
  pn1->data=x;
  pn1->next=pn2;
  pn2->data=y;
  pn2->next=nullptr;
  return pn1;
}
```

