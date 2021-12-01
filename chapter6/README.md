---
sort: 6
---
# 第六章
> 这章题目好多，终于赶完了，质量会差，但也应该不会找时间再看了，有什么问题都可以联系我。  
  
1. [DC06PE01 已知完全二叉树采用顺序存储结构，求编号i和j的两个结点的最近公共祖先结点的编号](#DC06PE01ij)
2. [DC06PE02 对于顺序结构的完全二叉树，判别结点v是否为结点u的子孙](#DC06PE02vu)
3. [DC06PE06 判别两棵二叉树是否相似。](#DC06PE06)
4. [DC06PE11 编写递归算法，求对二叉树T先序遍历时第k个访问的结点的值。](#DC06PE11Tk)
5. [DC06PE12 编写递归算法，计算二叉树T中叶子结点的数目。](#DC06PE12T)
6. [DC06PE21 利用栈及其基本操作，编写二叉树的非递归的先序遍历算法。](#DC06PE21)
7. [DC06PE23 试利用栈及其基本操作，编写二叉树的非递归的后序遍历算法](#DC06PE23)
8. [DC06PE27 二叉树采用三叉链表的存储结构，试编写不借助栈的非递归中序遍历算法。](#DC06PE27)
9. [DC06PE29 编写不用栈辅助的二叉树非递归后序遍历算法](#DC06PE29)
10. [DC06PE30 判别给定两棵二叉树是否相似](#DC06PE30)
11. [DC06PE31 利用栈的基本操作，写出先序遍历的非递归形式的算法](#DC06PE31)
12. [DC06PE32 利用栈的基本操作，写出后序遍历的非递归算法](#DC06PE32)
13. [DC06PE33 编写递归算法，将二叉树中所有结点的左、右子树相互交换。](#DC06PE33)
14. [DC06PE34 不使用栈，写出三叉链表的后序遍历的非递归算法](#DC06PE34)
15. [DC06PE35 不使用栈，写出三叉链表的中序遍历的非递归算法](#DC06PE35)
16. [DC06PE36 求以二叉链表存储的完全二叉树的最后一层的最后一个结点](#DC06PE36)
17. [DC06PE37 编写递归算法：求二叉树中以元素值为x的结点为根的子树的深度。](#DC06PE37x)
18. [DC06PE40 对二叉树中每一个结点x，删去以x为根的子树。](#DC06PE40xx)
19. [DC06PE43 编写复制一棵二叉树的递归算法。](#DC06PE43)
20. [DC06PE44 编写递归算法，求二叉树中以元素值为x的结点为根的子树的深度](#DC06PE44x)
21. [DC06PE45 编写递归算法，对于二叉树中每一个元素值为x的结点，删去以它为根的子树，并释放相应的空间](#DC06PE45x)
22. [DC06PE46 复制一棵二叉树（非递归，利用队列）](#DC06PE46)
23. [DC06PE47 利用队列的基本操作，编写按层次顺序(同一层自左至右)遍历二叉树的算法](#DC06PE47)
24. [DC06PE48 已知二叉树中的两个结点，求距离它们最近的共同祖先](#DC06PE48)
25. [DC06PE49 编写算法判别给定二叉树是否为完全二叉树](#DC06PE49)
26. [DC06PE50 判别两棵二叉树是否相等](#DC06PE50)
27. [DC06PE51 求二叉树中度为1的结点数目](#DC06PE511)
28. [DC06PE52 求二叉树的分支结点总数](#DC06PE52)
29. [DC06PE53 按层次遍历方式计算二叉树的结点个数](#DC06PE53)
30. [DC06PE54 对一棵二叉树，将它的所有没有左孩子但有右孩子的结点，将其右孩子改变为左孩子](#DC06PE54)
31. [DC06PE55 求二叉树的宽度](#DC06PE55)
32. [DC06PE56 编写递归算法，查找求二叉树T中是否存在元素值为x的结点](#DC06PE56Tx)
33. [DC06PE57 计算二叉树中值为x的结点所在的层次](#DC06PE57x)
34. [DC06PE58 求二叉树中以元素值为x的结点为根的子树的结点总数](#DC06PE58x)
35. [DC06PE59 求指定结点在二叉树中的层次](#DC06PE59)
36. [DC06PE60 判别一棵二叉树是否为正则二叉树](#DC06PE60)
37. [DC06PE61 判别一棵二叉树是否为小根二叉树](#DC06PE61)
38. [DC06PE62 利用队列，非递归求解二叉树的宽度](#DC06PE62)
39. [DC06PE65 试编写一个二叉排序树的判定算法。](#DC06PE65)
40. [DC06PE66 从大到小输出给定二叉排序树中所有关键字不小于x的数据元素](#DC06PE66x)
41. [DC06PE67 在二叉查找树中插入一个元素](#DC06PE67)
42. [DC06PE68 求二叉树T中任意两个结点的最近共同祖先。](#DC06PE68T)
43. [DC06PE75 求二叉排序树中第k小的结点的位置](#DC06PE75k)
44. [DC06PE77 求二叉排序树T的深度，并j记录每个结点平衡因子](#DC06PE77Tj)
45. [DC06PE82 平衡二叉排序树的右平衡处理](#DC06PE82)

##  1. <a name='DC06PE01ij'></a>DC06PE01 已知完全二叉树采用顺序存储结构，求编号i和j的两个结点的最近公共祖先结点的编号
```C
int commonAncestor(SqBiTree T, int i, int j) 
{  
  if(i>T.lastIndex || j>T.lastIndex || i<2 || j<2)//1号位没有祖先，所以至少要是2号位
    return 0;
  
  i/=2;//找i的父亲
  j/=2;//找j的父亲
  
  while(i!=j)
  {
    if(i>=j)
      i/=2;
    else
      j/=2;
  }
  return i;
}
```
##  2. <a name='DC06PE02vu'></a>DC06PE02 对于顺序结构的完全二叉树，判别结点v是否为结点u的子孙
```C
Status is_Desendant(SqBiTree T, int u, int v)  
{  
    //v结点是否是u结点的子孙
    if(u<1 || u>T.lastIndex || v<1 ||  v>T.lastIndex || v<=u)
      return FALSE;
  
    while(v>u)
    {
      v/=2;
    }
    if(u==v)
      return TRUE;
    return FALSE;
}
```
##  3. <a name='DC06PE06'></a>DC06PE06 判别两棵二叉树是否相似。
```C
Status Similar(BiTree T1, BiTree T2) 
{   
  if(T1==NULL || T2==NULL)
  {
    if(T1==NULL && T2==NULL)
      return TRUE;
    return FALSE;
  }
  int r1=Similar(T1->lchild, T2->lchild);
  int r2=Similar(T1->rchild, T2->rchild);
  return r1&&r2;
  /*
  比较两个节点都为空就相等、有一个为空，另一个非空则不相等。
  最后递归判断两个数的左子树和右子树是否相等。
  */
}
```
##  4. <a name='DC06PE11Tk'></a>DC06PE11 编写递归算法，求对二叉树T先序遍历时第k个访问的结点的值。
```C
TElemType PreOrderFindK(BiTree T, int &k) 
{
  TElemType result = '#';  
  if(T == NULL)
    return '#';
  if(k==1)
    return T->data;
  k--;
  if(T->lchild!=nullptr)
    result = PreOrderFindK(T->lchild, k);
  if(result == '#' && T->rchild!=nullptr)
    result =  PreOrderFindK(T->rchild, k);
  return result;
}
TElemType PreOrderK(BiTree T, int k) 
{
  return PreOrderFindK(T,k);
}
```
##  5. <a name='DC06PE12T'></a>DC06PE12 编写递归算法，计算二叉树T中叶子结点的数目。
```C
int Leaves(BiTree T) 
{   
  if (T==NULL)
    return 0;
  if(T->lchild==NULL && T->rchild==NULL)
    return 1;
  int r1 = Leaves(T->lchild);
  int r2 = Leaves(T->rchild);
  return r1+r2;
}
```
##  6. <a name='DC06PE21'></a>DC06PE21 利用栈及其基本操作，编写二叉树的非递归的先序遍历算法。
```C
void PreOrder(BiTree T, Status (*visit)(TElemType))
{  
    Stack S;
    InitStack(S);
    BiTree p=T;
    
    while (StackEmpty(S)!=TRUE || p!=NULL)//栈非空或p非空时
    {
        while(p)
        {
            visit(p->data);
            Push(S, p);
            p = p->lchild;
        }
        if (!StackEmpty(S))
        {
            Pop(S,p);
            p = p->rchild;
        }
    }
    return;
}
```
##  7. <a name='DC06PE23'></a>DC06PE23 试利用栈及其基本操作，编写二叉树的非递归的后序遍历算法
法一：
```C
//参考：https://blog.csdn.net/wayne_b/article/details/46276429
//tag: 0表示刚遍历完该节点的左子树，需要遍历右子树；1表示已经遍历完该节点左右子树
void GoFar(BiTree &T,Stack &S, Status (*visit)(TElemType))
{
    SElemType tmp; 
    while(T->lchild!=NULL || T->rchild!=NULL)
    {
        tmp.ptr = T;
        if(T->lchild != NULL && T->rchild !=NULL)       //还有右孩子，仍要继续遍历
        {           
            tmp.tag = 0;
            T = T->lchild;
        }
        else if(T->lchild != NULL && T->rchild == NULL)
        {
            tmp.tag = 1;
            T = T->lchild;
        }
        else if(T->rchild != NULL)                      //没有左孩子只有右孩子就深入右孩子
        {
            tmp.tag = 1;
            T = T->rchild;                         
        }
        Push(S,tmp);                                    //T节点入栈
    }
    visit(T->data);
    return;
}
void PostOrder(BiTree T, Status (*visit)(TElemType))
{
    if(T == NULL) 
      return;       
    Stack S;   
    InitStack(S);    
    SElemType e;
    BiTree p = T;
    
    GoFar(p, S, visit);                                //调用函数深入二叉树
    
    SElemType tmp;
    while(p != NULL && StackEmpty(S)!=TRUE)
    {
        Pop(S,tmp);                                     //祖先节点出栈
        p = tmp.ptr;
        if(tmp.tag == 0)                                //若刚遍历完该节点的左孩子
        {                               
            tmp.tag = 1;                                //有的话tag致1入栈
            Push(S, tmp);
            p = p->rchild;
            GoFar(p,S, visit);                         //且深入它的右子树继续遍历
        }
        else if(tmp.tag==1)
        {
            visit(p->data);                             //若已遍历完左右子树就访问自己
        }
    }
}
```
法二：
```C
void PostOrder(BiTree T, Status (*visit)(TElemType))
{ 
    if(T == NULL) 
      return;
    Stack S;   
    InitStack(S);    
    SElemType e;
    BiTree p = T;
    
    e.ptr=p;
    e.tag=0;
    Push(S,e);
    while(StackEmpty(S)!=TRUE)
    {
        Pop(S,e);
        if(e.tag==0)
        {    
            e.tag=1;
            Push(S,e); 
            
            if(e.ptr->lchild!=NULL)
            {
                e.ptr=e.ptr->lchild;
                e.tag=0;
                Push(S,e);
            }   
            continue;
        }
        if(e.tag==1)
        {
             e.tag=2;
             Push(S,e); 
             
             if(e.ptr->rchild!=NULL)
             {
                e.ptr=e.ptr->rchild;
                e.tag=0;
                Push(S,e);
             } 
             continue;
        }
        if(e.tag==2)
        {
             visit(e.ptr->data);        
        }    
    }
}*/
```
##  8. <a name='DC06PE27'></a>DC06PE27 二叉树采用三叉链表的存储结构，试编写不借助栈的非递归中序遍历算法。
```C
//参考：https://blog.csdn.net/qq1094417747/article/details/52831479
void InOrder(TriTree PT, Status (*visit)(TElemType)) 
{   
  TriTree p = PT, pChild;
    
  while(p!=NULL)  
  {  
    if(p->lchild!=NULL) 
    {
      p = p->lchild;
      continue;
    }
    visit(p->data); 
    if (p->rchild!=NULL) 
    {  
        p =p->rchild;    
        continue;
    }   
    pChild = p;   
    p = p->parent;  
    while (p && (p->lchild != pChild ||!p->rchild)) //若其不是从左子树回溯来的，或左结点的父亲并没有右孩子
    {  
      if (p->lchild == pChild)  //若左结点的父亲并没有右孩子        
        visit(p->data);   //直接访问父亲（不用转到右孩子）             
        pChild = p;  //父亲已被访问，故返回上一级
        p = p->parent;  //该while循环沿双亲链一直查找，若无右孩子则访问，直至找到第一个有右孩子的结点为止（但不访问该结点，留给下步if语句访问）
      }  
      if (p) 
      {   //访问父亲，并转到右孩子（经上步while处理，可以确定此时p有右孩子）
        visit(p->data);
        p = p->rchild;  
      }  
    }  
}
```
##  9. <a name='DC06PE29'></a>DC06PE29 编写不用栈辅助的二叉树非递归后序遍历算法
```C
void PostOrder(TriTree T, Status (*visit)(TElemType)) 
{   
    TriTree p = T;

    while (p != NULL)
    {
        if (p->mark == 0)
        {
            p->mark++;
            while (p->lchild != NULL)
            {
                p = p->lchild;
                p->mark++;
            }
            continue;
        }
        if (p->mark == 1)
        {
            p->mark++;
            if (p->rchild != NULL)
                p = p->rchild;
            continue;
        }
        if (p->mark == 2)
        {
            visit(p->data);
            p = p->parent;
        }
    }
}
```
##  10. <a name='DC06PE30'></a>DC06PE30 判别给定两棵二叉树是否相似
```C
Status Similar(BiTree t1, BiTree t2) 
{   
  if(t1==NULL || t2==NULL)
  {
    if(t1==NULL && t2==NULL)
      return TRUE;
    return FALSE;
  }
  int r1=Similar(t1->lchild, t2->lchild);
  int r2=Similar(t1->rchild, t2->rchild);
  return r1&&r2;
}
```
##  11. <a name='DC06PE31'></a>DC06PE31 利用栈的基本操作，写出先序遍历的非递归形式的算法
```C
void PreOrder(BiTree bt, void (*visit)(TElemType)) 
{
    SqStack2 S;
    InitStack_Sq2(S);
    
    BiTree p = bt;
    while(StackEmpty_Sq2(S)!=TRUE || p!=NULL)
    {
      while(p!=NULL)
      {
        visit(p->data);
        Push_Sq2(S, p);        
        p=p->lchild;
      }
      
      if(!StackEmpty_Sq2(S))
      {
        Pop_Sq2(S, p);
        p=p->rchild;
      }
    }
    return;
}
```
##  12. <a name='DC06PE32'></a>DC06PE32 利用栈的基本操作，写出后序遍历的非递归算法
```C
void PostOrder(BiTree bt, void (*visit)(TElemType))
{
    if(bt == NULL) 
      return;
    SqStack2 S;   
    InitStack_Sq2(S);    
    SElemType e;
    BiTree p = bt;
    
    e.ptr=p;
    e.tag=0;//e.tag=p->mark;
    Push_Sq2(S,e);
    while(!StackEmpty_Sq2(S))
    {
        Pop_Sq2(S,e);
        if(e.tag==0)
        {    
            e.tag=1;
            Push_Sq2(S,e); 
            
            if(e.ptr->lchild!=NULL)
            {
                e.ptr=e.ptr->lchild;
                e.tag=0;
                Push_Sq2(S,e);
            }   
            continue;
        }
        if(e.tag==1)
        {
             e.tag=2;
             Push_Sq2(S,e); 
             
             if(e.ptr->rchild!=NULL)
             {
                e.ptr=e.ptr->rchild;
                e.tag=0;
                Push_Sq2(S,e);
             } 
             continue;
        }
        if(e.tag==2)
        {
             visit(e.ptr->data);        
        }    
    }
}
```
##  13. <a name='DC06PE33'></a>DC06PE33 编写递归算法，将二叉树中所有结点的左、右子树相互交换。
```C
void ExchangeSubTree(BiTree &T)
{   
    if(T!=NULL)
    {
      BiTree tempT=T->lchild;
      T->lchild=T->rchild;
      T->rchild=tempT;
      ExchangeSubTree(T->lchild);
      ExchangeSubTree(T->rchild);
    }
}
```
##  14. <a name='DC06PE34'></a>DC06PE34 不使用栈，写出三叉链表的后序遍历的非递归算法
```C
void PostOrder(TriTree bt, void (*visit)(TElemType))
/* 不使用栈，非递归后序遍历二叉树bt，  */
/* 对每个结点的元素域data调用函数visit */
{
    TriTree p = bt;

    while (p != NULL)
    {
        if (p->mark == 0)
        {
            p->mark++;
            while (p->lchild != NULL)
            {
                p = p->lchild;
                p->mark++;
            }
            continue;
        }
        if (p->mark == 1)
        {
            p->mark++;
            if (p->rchild != NULL)
                p = p->rchild;
            continue;
        }
        if (p->mark == 2)
        {
            visit(p->data);
            p = p->parent;
        }
    }
}
```
##  15. <a name='DC06PE35'></a>DC06PE35 不使用栈，写出三叉链表的中序遍历的非递归算法
```C
void InOrder(TriTree PT, void (*visit)(TElemType))
/* 不使用栈，非递归中序遍历二叉树bt，  */
/* 对每个结点的元素域data调用函数visit */
{  
    TriTree p = PT;

    while (p != NULL)
    {
        if (p->mark == 0)
        {
            p->mark++;
            while (p->lchild != NULL)
            {
                p = p->lchild;
                p->mark++;
            }
            continue;
        }
        if (p->mark == 1)
        {
            p->mark++;
            visit(p->data);
            if (p->rchild != NULL)
                p = p->rchild;
            continue;
        }
        if (p->mark == 2)
        {            
            p = p->parent;
        }
    }
}
```
##  16. <a name='DC06PE36'></a>DC06PE36 求以二叉链表存储的完全二叉树的最后一层的最后一个结点
```C
BiTNode* getLastNode(BiTree T)
/* 求完全二叉树的最后一层的最后一个结点 */
{   
    if(T==NULL || (T->lchild==NULL&&T->rchild==NULL))
      return T;
    //求二叉树深度
    int dep=0;
    BiTree curNode = T;
    while(curNode!=NULL)
    {
      dep++;
      curNode = curNode->lchild;
    }
    

    int level = 0;
    BiTree p = T;
  	while(p)//控制p下一步往右还是往左走
  	{
  		level++;//level: 当前的层数
  		if(level == dep)  break;//当前是最后一层，退出。
  		curNode = p;
  		
  		if(curNode->rchild!=NULL)//当前结点的右孩子是否存在
  		{
  		  BiTree pPar = curNode;//pPar: 当前节点的父节点
  		  curNode = curNode -> rchild;
  		  int tmpDep = level + 1;//tmp:当前深度。往右走之后深度为level加一
  		  
  			while(curNode->lchild)//找到右孩子后一直往左走
  			{
  				tmpDep++;
  				pPar = curNode;
  				curNode = curNode->lchild;
  			}
  			//curNode: 当前找到的目标结点
  			
  			if(tmpDep < dep)//说明p往右走不对。往左走
  			  p = p->lchild;  			
  			else if(tmpDep == dep && (pPar->rchild != NULL && pPar->rchild != curNode))
  			  p = p->rchild;
  			else if(tmpDep == dep && (pPar->rchild == NULL || pPar->rchild == curNode))
  			  return curNode;
  		}
  		else p = p->lchild;//右孩子不存在，直接往左走
  	}
    return p;
}
```
##  17. <a name='DC06PE37x'></a>DC06PE37 编写递归算法：求二叉树中以元素值为x的结点为根的子树的深度。
```C
int BiTreeDepth(BiTree T)
{
    if(T==NULL)
      return 0;
    int r1 = BiTreeDepth(T->lchild);
    int r2 = BiTreeDepth(T->rchild);
    return 1 + (r1 > r2 ? r1 : r2);
}

int Depthx(BiTree T, TElemType x)
{  
  if(T==NULL)
    return 0;
  if(T->data==x)
    return BiTreeDepth(T);
  int r1=Depthx(T->lchild,x);
  int r2=Depthx(T->rchild,x);
  return r1>r2?r1:r2;
}
```
##  18. <a name='DC06PE40xx'></a>DC06PE40 对二叉树中每一个结点x，删去以x为根的子树。
```C
void NodesDel(BiTree &bt)
{
    if(bt==NULL)
      return;
    NodesDel(bt->lchild);
    NodesDel(bt->rchild);
    free(bt);
    return;
}
void ReleaseX(BiTree &bt, char x)
{  
    BiTree p=NULL;
    if (bt == NULL)
      return;
    if(bt->data==x)
    {
      p = bt;
      bt = NULL;
      NodesDel(p);
    }
   
    if(bt!=NULL)
    {
      ReleaseX(bt->lchild, x);
    }
    if(bt!=NULL)
    {
      ReleaseX(bt->rchild, x);
    }
    return;
}
```
##  19. <a name='DC06PE43'></a>DC06PE43 编写复制一棵二叉树的递归算法。
```C
void CopyBiTree(BiTree T, BiTree &TT)      
{   
    if(T==NULL)
        return;
        
    BiTree p = (BiTree)malloc(sizeof(BiTNode));
    p->data = T->data;
    p->lchild=T->lchild;
    p->rchild=T->rchild;
    TT = p;
    CopyBiTree(T->lchild,p->lchild);
    CopyBiTree(T->rchild,p->rchild);
}
```
##  20. <a name='DC06PE44x'></a>DC06PE44 编写递归算法，求二叉树中以元素值为x的结点为根的子树的深度
```C
int BiTreeDepth(BiTree T)
{
  int depthLeft, depthRight;
  if(T==NULL)
    return 0;
  else
  {
    depthLeft = BiTreeDepth(T->lchild);
    depthRight = BiTreeDepth(T->rchild);
    return 1+(depthLeft>depthRight?depthLeft:depthRight);
  }
}
int Depthx(BiTree T, TElemType x)
{  
  if(T==NULL)
    return 0;
  if(T->data==x)
    return BiTreeDepth(T);
  int r1=Depthx(T->lchild,x);
  int r2=Depthx(T->rchild,x);
  return r1>r2?r1:r2;
}
```
##  21. <a name='DC06PE45x'></a>DC06PE45 编写递归算法，对于二叉树中每一个元素值为x的结点，删去以它为根的子树，并释放相应的空间
```C
void NodesDel(BiTree &bt)
{
    if(bt==NULL)
      return;
    NodesDel(bt->lchild);
    NodesDel(bt->rchild);
    free(bt);
    return;
}
void ReleaseX(BiTree &bt, char x)
{  
    BiTree p=NULL;
    if (bt == NULL)
      return;
    if(bt->data==x)
    {
      p = bt;
      bt = NULL;
      NodesDel(p);
    }
   
    if(bt!=NULL)
    {
      ReleaseX(bt->lchild, x);
    }
    if(bt!=NULL)
    {
      ReleaseX(bt->rchild, x);
    }
    return;
}
```
##  22. <a name='DC06PE46'></a>DC06PE46 复制一棵二叉树（非递归，利用队列）
```C
void CopyBiTree(BiTree T, BiTree &TT)
{  
  if(T==NULL)
    return;
  BiTree p1 = T;

  //复制根结点
  BiTree p2 = (BiTree)malloc(sizeof(BiTNode));
  memset(p2, 0, sizeof(BiTNode));
  p2->data = p1->data;
  TT = p2;
  
  LQueue Q,Q2;
  InitQueue_LQ(Q);
  InitQueue_LQ(Q2);
  
  EnQueue_LQ(Q,p1);
  EnQueue_LQ(Q2,p2);
  while(!QueueEmpty_LQ(Q))
  {
    DeQueue_LQ(Q,p1);
    DeQueue_LQ(Q2,p2);
    if(p1->lchild!=NULL)
    {
      BiTree pNode = (BiTree)malloc(sizeof(BiTNode));
      memset(pNode, 0, sizeof(BiTNode));
      p2->lchild = pNode;
      p2->lchild->data = p1->lchild->data;
      EnQueue_LQ(Q,p1->lchild);
      EnQueue_LQ(Q2,p2->lchild);
    }
    if(p1->rchild!=NULL)
    {
      BiTree pNode = (BiTree)malloc(sizeof(BiTNode));
      memset(pNode, 0, sizeof(BiTNode));
      p2->rchild = pNode;
      p2->rchild->data = p1->rchild->data;
      EnQueue_LQ(Q,p1->rchild);
      EnQueue_LQ(Q2,p2->rchild);
    }
  }
}
```
##  23. <a name='DC06PE47'></a>DC06PE47 利用队列的基本操作，编写按层次顺序(同一层自左至右)遍历二叉树的算法
```C
void LevelOrder(BiTree bt, char *ss)
{ 
  if(bt == NULL)
    return;
  BiTree p =bt;
  char sp[2]={0};
  LQueue Q;
  InitQueue_LQ(Q);
  
  EnQueue_LQ(Q,p);
  while(!QueueEmpty_LQ(Q))
  {
    DeQueue_LQ(Q,p);
    sprintf(sp,"%c",p->data);
    strcat(ss,sp);
    if(p->lchild!=NULL)
    {
      EnQueue_LQ(Q,p->lchild);
    }
    if(p->rchild!=NULL)
    {
      EnQueue_LQ(Q,p->rchild);
    }
  }
/*  int len = strlen(ss);
  ss[len]={0};*/  
}
```
##  24. <a name='DC06PE48'></a>DC06PE48 已知二叉树中的两个结点，求距离它们最近的共同祖先
```C
//参考：https://blog.csdn.net/wayne_b/article/details/46276429
bool FindPath(BiTree T, TElemType c, SqStack2& S)
{
  if(T==NULL)
    return FALSE;
  if(T->data == c)
    return TRUE;
  SElemType tmp;
  tmp.tag = 0;
  if(FindPath(T->lchild, c, S)|| FindPath(T->rchild, c, S))
  {
    tmp.ptr = T;
    Push_Sq2(S, tmp);
  }
  else return FALSE;
  return TRUE;
}

BiTree CommAncestor(BiTree root, TElemType c1, TElemType c2)
{
    if(root == NULL || c1==root->data || c2==root->data) 
      return NULL;       
      
    SqStack2 S1, S2;   
    InitStack_Sq2(S1);  
    InitStack_Sq2(S2);  
    
    if(FindPath(root, c1, S1)==FALSE)
      return NULL;
    if(FindPath(root, c2, S2)==FALSE)
      return NULL;  
    
    SElemType par1, par2, par;
    do{
      par = par1;
      Pop_Sq2(S1, par1);
      Pop_Sq2(S2, par2);
    }while(StackEmpty_Sq2(S1)!=TRUE && StackEmpty_Sq2(S2)!=TRUE && par1.ptr==par2.ptr);
    if(par1.ptr==par2.ptr)
      return par1.ptr;
    else return par.ptr;
}
```
##  25. <a name='DC06PE49'></a>DC06PE49 编写算法判别给定二叉树是否为完全二叉树
```C
Status CompleteBiTree(BiTree bt)
{  
  if(bt == NULL)
    return TRUE;
  
  BiTree p = bt;
  LQueue Q;
  InitQueue_LQ(Q);
  while(p!=NULL)//一层一层遍历，知道遇到第一个NULL
  {
    EnQueue_LQ(Q, p->lchild);
    EnQueue_LQ(Q, p->rchild);
    DeQueue_LQ(Q, p);
  }
  while(!QueueEmpty_LQ(Q))//遇到NULL后，队列里都要是NULL
  {
    DeQueue_LQ(Q, p);
    if(p!=NULL)
    {
      if(p->data!=NULL)
        return FALSE;
    }
  }
  return TRUE;
}
```
##  26. <a name='DC06PE50'></a>DC06PE50 判别两棵二叉树是否相等
```C
Status  BTEqual(BiTree T1, BiTree T2)
{  
  if(T1==NULL||T2==NULL)
  {
    if(T1==NULL && T2==NULL)
      return TRUE;
    return FALSE;
  }
  else if(T1->data==T2->data)
  {
    return TRUE;
  }
  else 
  {
    return FALSE;
  }
  Status r1 = BTEqual(T1->lchild,T2->lchild);
  Status r2 = BTEqual(T1->lchild,T2->rchild);
  return r1&&r2;
}
```
##  27. <a name='DC06PE511'></a>DC06PE51 求二叉树中度为1的结点数目
```C
void Degree1(BiTree T,int &count)
{  
  //一个结点的度是这个结点含有子树的个数
  if(T==NULL)
    return;
  if(T->lchild!=NULL || T->rchild!=NULL)
  {
    if(T->lchild!=NULL&&T->rchild!=NULL)
    {
      ;
    }
    else{
      count++;
    }
  }
    Degree1(T->lchild,count);
    Degree1(T->rchild,count);
    return;
}
```
##  28. <a name='DC06PE52'></a>DC06PE52 求二叉树的分支结点总数
```C
void NodesCount(BiTree T, int& count)
{
  //分支结点：一个二叉树中度不为0的结点
  if(T==NULL)
      return;
  if(T->lchild!=NULL || T->rchild!=NULL)
  {
    if(T->lchild!=NULL && T->rchild!=NULL)
      ;
    count++;
  }
  NodesCount(T->lchild,count);
  NodesCount(T->rchild,count);
}
int BranchNodes(BiTree T)
{  
    int count=0;
    NodesCount(T, count);
    return count;
}
```
##  29. <a name='DC06PE53'></a>DC06PE53 按层次遍历方式计算二叉树的结点个数
```C
int LevelSum(BiTree T)
{ 
    int count = 0;
    if(T==NULL)
      return count;
    count++;
    LQueue Q;
    InitQueue_LQ(Q);
    BiTree p = T;
    
    EnQueue_LQ(Q,p);
    do
    {
      DeQueue_LQ(Q,p);
      if(p->lchild!=NULL)
      {
        count++;
        EnQueue_LQ(Q,p->lchild);
      }
      if(p->rchild!=NULL)
      {
        count++;
        EnQueue_LQ(Q,p->rchild);
      }
    }while(!QueueEmpty_LQ(Q));
    
    return count;
}
```
##  30. <a name='DC06PE54'></a>DC06PE54 对一棵二叉树，将它的所有没有左孩子但有右孩子的结点，将其右孩子改变为左孩子
```C
void ChangeTree(BiTree &T)
{  
  if(T==NULL)
    return;
  if(T->lchild==NULL && T->rchild !=NULL)
  {
    T->lchild=T->rchild;
    T->rchild=NULL;
  }
  ChangeTree(T->lchild);
  ChangeTree(T->rchild);
}
```
##  31. <a name='DC06PE55'></a>DC06PE55 求二叉树的宽度
```C
//参考：https://blog.csdn.net/u013709443/article/details/81212915
int BiTreeDepth(BiTree T)
{
    if(T==NULL)
      return 0;
    int r1 = BiTreeDepth(T->lchild);
    int r2 = BiTreeDepth(T->rchild);
    return 1 + (r1 > r2 ? r1 : r2);
}

int LevelWidth(BiTree T, int level)
{
	if(T == NULL)
	  return 0;//空，宽度为0
	if(level == 1)
	  return 1;//宽度为1
	level = LevelWidth(T->lchild,level-1) + LevelWidth(T->rchild,level-1);
	return level;
}

int Width(BiTree T)
{
  if(T==NULL)
	  return 0;
	int maxWid=0,wid;
	int dep = BiTreeDepth(T);
	for(int i=1; i<=dep+1; i++)
	{
	  wid = LevelWidth(T,i);
	  if(wid > maxWid)
	  {
	    maxWid = wid;
	  }
	}
	return maxWid;
}
```
##  32. <a name='DC06PE56Tx'></a>DC06PE56 编写递归算法，查找求二叉树T中是否存在元素值为x的结点
```C
Status SearchX(BiTree T, TElemType x)
{  
  if(T==NULL)
    return ERROR;
  if(T->data==x)
    return TRUE;
  Status r1 = SearchX(T->lchild,x);
  Status r2 = SearchX(T->rchild,x);
  return r1||r2;
}
```
##  33. <a name='DC06PE57x'></a>DC06PE57 计算二叉树中值为x的结点所在的层次
```C
int NodeLevel(BiTree t, TElemType x)
{  
  if(t==NULL)
    return -1;
  if(t->data==x)
    return 1;
  int r1 = NodeLevel(t->lchild,x);
  int r2 = NodeLevel(t->rchild,x);
  if(r1!=-1||r2!=-1)
    return (r1>r2)?r1+1:r2+1;
  return -1;
}
```
##  34. <a name='DC06PE58x'></a>DC06PE58 求二叉树中以元素值为x的结点为根的子树的结点总数
```C
void NodesCount(BiTree T, int& count)
{
  //一个子树所有结点
  if(T==NULL)
      return;
  count++;
  NodesCount(T->lchild,count);
  NodesCount(T->rchild,count);
}
int xSum(BiTree T, TElemType x)
{  
    if(T==NULL)
      return 0;
    if(T->data==x)
    {
      int count=0;
      NodesCount(T, count);
      return count;
    }
    int r1 = xSum(T->lchild,x);
    int r2 = xSum(T->rchild,x);
    return r1 | r2;
}
```
##  35. <a name='DC06PE59'></a>DC06PE59 求指定结点在二叉树中的层次
```C
void xLevel(BiTree T,TElemType x, bool &found, int &xlev)
{ 
    if(T==NULL)
      return;
      
    found=false;
    xlev++;
    if(T->data==x)
    {
      found = true;
      return;
    }

    int tmp=xlev;
    xLevel(T->lchild,x,found,xlev);
    if(found==0)
    {
      xlev= tmp;
      xLevel(T->rchild,x,found,xlev);
    }
    else return;
}
```
##  36. <a name='DC06PE60'></a>DC06PE60 判别一棵二叉树是否为正则二叉树
```C
Status RegularBiTree(BiTree T)
{  
  if(T==NULL)
    return FALSE;
  if(T->lchild!=NULL||T->rchild!=NULL)
  {
    if(T->lchild!=NULL&&T->rchild!=NULL)
      ; 
    return FALSE;
  }
  return TRUE;
  Status r1 = RegularBiTree(T->lchild);
  Status r2 = RegularBiTree(T->rchild);
  return r1&&r2;
}
```
##  37. <a name='DC06PE61'></a>DC06PE61 判别一棵二叉树是否为小根二叉树
```C
Status SmallBiTree(BiTree T)
{ 
  if(T==NULL)
    return OK;
  Status r1=OK;
  Status r2=OK;
  if(T->lchild!=NULL && T->lchild->data >= T->data)
  {
      return ERROR;
  }
  if(T->rchild!=NULL && T->rchild->data >= T->data)
  {
      return ERROR;
  }
  r1=SmallBiTree(T->lchild);
  r2=SmallBiTree(T->rchild);
  return r1&&r2;
}
```
##  38. <a name='DC06PE62'></a>DC06PE62 利用队列，非递归求解二叉树的宽度
```C
int Width(BiTree T)
{
  if(T==NULL)
    return 0;
    
  LQueue Q;
  ElemType e;
  int maxWid=-1;
  int lcount;//上一层的节点数，宽度
  int count;//这一层的节点数，宽度
  InitQueue_LQ(Q);
  EnQueue_LQ(Q,T);
  lcount = 1;
  
  while(QueueEmpty_LQ(Q)!=TRUE)
  {
    count = 0;
    for(int i=0;i<lcount;i++)
    {
      DeQueue_LQ(Q, e);
      if(e->lchild!=NULL)
      {
        EnQueue_LQ(Q,e->lchild);
        count++;
      }
      if(e->rchild!=NULL)
      {
        EnQueue_LQ(Q,e->rchild);
        count++;
      }
    }
    if(count>maxWid)
      maxWid = count;
    lcount = count;
  }
  return maxWid;
}
```
##  39. <a name='DC06PE65'></a>DC06PE65 试编写一个二叉排序树的判定算法。
```C
Status IsBSTree(BSTree T) 
{  
  if(T==NULL)
    return OK;
  Status r1 = OK;
  Status r2 = OK;
  if(T->lchild!=NULL)
  {
    if(T->data.key < T->lchild->data.key)
      return FALSE;
    r1 = IsBSTree(T->lchild);
  }
  
  if(T->rchild!=NULL)
  {
    if(T->data.key > T->rchild->data.key)
      return FALSE;
    r2 = IsBSTree(T->rchild);
  }
  return r1&&r2;
}
```
##  40. <a name='DC06PE66x'></a>DC06PE66 从大到小输出给定二叉排序树中所有关键字不小于x的数据元素
```C
void OrderOut(BSTree T, KeyType k, void(*visit)(TElemType))
{   
  if(T==NULL)
    return;
  //先访问右结点，然后访问根结点，然后访问左结点。
  OrderOut(T->rchild,k,visit);
  if(T->data.key>=k)
    visit(T->data);
  OrderOut(T->lchild,k,visit);
}
```
##  41. <a name='DC06PE67'></a>DC06PE67 在二叉查找树中插入一个元素
```C
Status InsertBST_I(BSTree &T, TElemType k) 
{    
  BSTree pNode = (BSTree)malloc(sizeof(BSTNode));
  memset(pNode,0,sizeof(BSTNode));
  pNode->data = k;
  if(T==NULL)
  {
    T=pNode;
    return OK;
  }
  BSTree p = T;

  while(1)
  {
      if(p->data.key == k.key)
      {
        return ERROR; 
      }
      if(p->data.key > k.key)
      {
        if(p->lchild!=NULL&&p->lchild->data.key != NULL)
          p = p->lchild;
        else
        {
          p->lchild=pNode;
          return OK;
        }
      }
      else if(p->data.key < k.key)
      {
        if(p->rchild!=NULL&&p->rchild->data.key != NULL)
          p = p->rchild;
        else
        {
          p->rchild=pNode;
          return OK;
        }
      }
  }
}
```
##  42. <a name='DC06PE68T'></a>DC06PE68 求二叉树T中任意两个结点的最近共同祖先。
```C
bool FindPath(BiTree T, TElemType c, Stack& S)
{
  if(T==NULL)
    return FALSE;
  if(T->data == c)
    return TRUE;
  SElemType tmp;
  tmp.tag = 0;
  if(FindPath(T->lchild, c, S)|| FindPath(T->rchild, c, S))
  {
    tmp.ptr = T;
    Push(S, tmp);
  }
  else return FALSE;
  return TRUE;
}

BiTree CommAncestor(BiTree root, TElemType a, TElemType b)
{
    if(root == NULL || a==root->data || b==root->data) 
      return NULL;       
      
    Stack S1, S2;   
    InitStack(S1);  
    InitStack(S2);  
    
    if(FindPath(root, a, S1)==FALSE)
      return NULL;
    if(FindPath(root, b, S2)==FALSE)
      return NULL;  
    
    SElemType par1, par2, par;
    do{
      par = par1;
      Pop(S1, par1);
      Pop(S2, par2);
    }while(StackEmpty(S1)!=TRUE && StackEmpty(S2)!=TRUE && par1.ptr==par2.ptr);
    if(par1.ptr==par2.ptr)
      return par1.ptr;
    else return par.ptr;
}
```
##  43. <a name='DC06PE75k'></a>DC06PE75 求二叉排序树中第k小的结点的位置
```C
BSTNode *Ranking(BSTree T, int k) 
{ 
    //第k小的结点左子树有k-1个结点
    //那么lsize==k的话，说明这个结点是第k小结点
    if(T==NULL)
      return ERROR;
    if(T->lsize == k)
        return T;
    if(T->lsize > k)
        return Ranking(T->lchild,k);
    if(T->lsize < k)
        return Ranking(T->rchild,k - T->lsize);//减去左子树T->lsize-1包括结点T一共T->lsize个结点 
}
```
##  44. <a name='DC06PE77Tj'></a>DC06PE77 求二叉排序树T的深度，并j记录每个结点平衡因子
```C
int Depth_BF(BBSTree T) 
{   
    if(T==NULL)
      return 0;
    int r1 = Depth_BF(T->lchild);
    int r2 = Depth_BF(T->rchild);
    T->bf = r1-r2;
    return 1 + (r1 > r2 ? r1 : r2);
}
```
##  45. <a name='DC06PE82'></a>DC06PE82 平衡二叉排序树的右平衡处理
```C
void RightBalance(BBSTree &T) 
{   
    BBSTree rc,ld;
    rc = T->rchild;
    switch(rc->bf)
    {
      case RH:
        T->bf = rc->bf = EH; 
        L_Rotate(T);
        break;
      case LH:
        ld = rc->lchild;
        switch(ld->bf)
        {
          case LH: T->bf = EH; rc->bf = LH; break;
          case EH: T->bf = rc->bf = EH; break;
          case RH: T->bf = RH; rc->bf = EH; break;
        }
        ld->bf = EH;
        R_Rotate(T->rchild);
        L_Rotate(T);
        break;
    }
}
```