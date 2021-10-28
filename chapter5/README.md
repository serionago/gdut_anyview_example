# 第五章
* 1. [DC05PE04 根据给定的递归函数，编写递归算法](#DC05PE04)
* 2. [DC05PE05 根据给定的递归函数F(n)编写递归算法](#DC05PE05Fn)
* 3. [DC05PE06 利用递归算法求解平方根](#DC05PE06)
* 4. [DC05PE07 请写出Ackerman函数的递归求解算法](#DC05PE07Ackerman)
* 5. [DC05PE15 试写出求递归函数F(n)的非递归算法](#DC05PE15Fn)
* 6. [DC05PE16 试写出求解平方根的非递归算法](#DC05PE16)
* 7. [DC05PE20 将给定点元素同色区域的颜色进行置换](#DC05PE20)
* 8. [DC05PE30 求广义表的深度](#DC05PE30)
* 9. [DC05PE32 判别两个广义表是否相等](#DC05PE32)
* 10. [DC05PE33 输出广义表中所有原子项及其所在的层次](#DC05PE33) 

##  1. <a name='DC05PE04'></a>DC05PE04 根据给定的递归函数，编写递归算法 
```C
int G(int m, int n) 
{ 
    if(m<0||n<0)
      return -1;
    if(m==0)
      return 0;
    return G(m-1,2*n)+n;
}
```
##  2. <a name='DC05PE05Fn'></a>DC05PE05 根据给定的递归函数F(n)编写递归算法
```C
int F(int n) 
{  
    if(n<0)
      return -1;
    if(n==0)
      return 1;
    return n*F(n/2);
}
```
##  3. <a name='DC05PE06'></a>DC05PE06 利用递归算法求解平方根
```C
float Sqrt(float A, float p, float e) 
{  
    if(abs(p*p-A)<e)
      return p;
    return Sqrt(A,(p+A/p)/2,e);
}
```
##  4. <a name='DC05PE07Ackerman'></a>DC05PE07 请写出Ackerman函数的递归求解算法
```C
int Akm(int m, int n) 
{  
  if(m<0||n<0)
    return -1;
  if(m==0)
    return n+1;
  if(m!=0&&n==0)
    return Akm(m-1,1);
  return Akm(m-1,Akm(m,n-1));
}
```
##  5. <a name='DC05PE15Fn'></a>DC05PE15 试写出求递归函数F(n)的非递归算法
```C
int F(int n) 
{ 
  if(n<0)
    return -1;//ERROR ARGUMENT
  if(n==0)
    return 1;
  
  //F(n)=n*F(n/2)
  //F(1)=1*F(0)=1*1=1
  //F(8)=8*F(4)=8*4*F(2)=8*4*2*F(1)=8*4*2*1*F(0)=8*4*2*1*1
  int result=n;//result当作F(n)
  while(n/=2)
  {
    result*=n;
  }
  return result;
}
```
##  6. <a name='DC05PE16'></a>DC05PE16 试写出求解平方根的非递归算法
牛顿迭代法：
```C
float Sqrt(float A, float p, float e) 
{
    if(p==0)
      return ERROR;
    while(abs(p*p-A)>=e)
    {
      p=(p+A/p)/2;
    }
    return p;
    //牛顿迭代法：https://blog.csdn.net/u010947534/article/details/87874019
}
```
迭代：
```C
float Sqrt(float A, float p, float e) 
{
    if(abs(p*p-A)<e)
      return p;
    while(abs(p*p-A)>=e)
    {
      p=(p+A/p)/2;
    }
    return p;
}
```
##  7. <a name='DC05PE20'></a>DC05PE20 将给定点元素同色区域的颜色进行置换
```C
void ChangeColor(GTYPE g, int m, int n, char c, int i0, int j0) 
{ 
  int tmp=g[i0][j0];//原来的颜色
  g[i0][j0]=c;//新的颜色

  if(i0-1>=0 && g[i0-1][j0]==tmp) ChangeColor(g, m, n, c, i0-1, j0);
  if(i0+1<=m && g[i0+1][j0]==tmp) ChangeColor(g, m, n, c, i0+1, j0);
  if(j0-1>=0 && g[i0][j0-1]==tmp) ChangeColor(g, m, n, c, i0, j0-1);
  if(j0+1<=n && g[i0][j0+1]==tmp) ChangeColor(g, m, n, c, i0, j0+1);
  return;
}
```
##  8. <a name='DC05PE30'></a>DC05PE30 求广义表的深度
```C
int GListDepth(GList ls) 
{ 
  int h1,h2;
  if(ls==nullptr)
    return 1;//空表，深度为1
  if(ls->tag==ATOM)
    return 0;//是一个原子，深度为0
  h1=GListDepth(ls->un.ptr.hp)+1;//表头的深度加1
  h2=GListDepth(ls->un.ptr.tp);//表尾的深度不需要加1，表尾的深度与原表相同
  return h1>=h2?h1:h2;
}
```
##  9. <a name='DC05PE32'></a>DC05PE32 判别两个广义表是否相等
```C
Status Equal(GList A, GList B) 
{ 
  if(A==nullptr || B==nullptr )
  {
    if(A==nullptr && B==nullptr)  
      return TRUE;
    else return FALSE;
  }
  
  if(A->tag==ATOM || B->tag==ATOM)
  {
    if(A->tag==ATOM && B->tag==ATOM && A->un.atom==B->un.atom)  
      return TRUE;
    //要先A->tag==ATOM、B->tag==ATOM都满足才能进行A->un.atom==B->un.atom的判断，否则可能会非法访问内存
    else return FALSE;
  }
  
  int r1 = Equal(A->un.ptr.hp,B->un.ptr.hp);
  int r2 = Equal(A->un.ptr.tp,B->un.ptr.tp);
  
  return r1&&r2;
}
```
##  10. <a name='DC05PE33'></a>DC05PE33 输出广义表中所有原子项及其所在的层次
```C
void OutAtom(GList A, int layer, void(*Out2)(char, int)) 
{ 
  //layer一开始是0
  //若广义表里只有一个原子A，这时A所在层数为0
  if(A==nullptr)
    return;
    
  if(A->tag==ATOM)
  {
    Out2(A->un.atom, layer);
    return;
  }
  
  OutAtom(A->un.ptr.hp, layer+1, Out2);
  OutAtom(A->un.ptr.tp, layer, Out2);
}
```
