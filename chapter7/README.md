# 第七章
* 1. [ DC07PE15 试编写算法，对一棵以孩子兄弟链表表示的树统计叶子的个数](#DC07PE15)
* 2. [ DC07PE17 求以孩子兄弟链表表示的树的度](#DC07PE17)
* 3. [ DC07PE22 计算以双亲表示法存储的树的深度](#DC07PE22)
* 4. [ DC07PE24 计算以双亲孩子表示法存储的树的深度](#DC07PE24)
* 5. [ DC07PE26 计算以孩子-兄弟链表表示的树的深度](#DC07PE26-)
* 6. [ DC07PE63 实现并查集带路径压缩的查找操作](#DC07PE63)

##  1. <a name='DC07PE15'></a> DC07PE15 试编写算法，对一棵以孩子兄弟链表表示的树统计叶子的个数 
```C
int Leave(CSTree T) 
{   
    if (T==NULL)
      return 0;
    //叶子：firstChild和nextSibling都为空；或firstChild为空nextSibling不为空。
    if(T->nextSibling==NULL&& T->firstChild==NULL)
      return 1;
    int res = 0; 
    
    if (T->nextSibling==NULL&&T->firstChild!=NULL) 
    {
      res += Leave(T->firstChild);
    }
    else  if (T->nextSibling!=NULL&&T->firstChild==NULL) 
    {
      res += Leave(T->nextSibling)+1;   
    }
    else if (T->nextSibling!=NULL&&T->firstChild!=NULL)
    {
      res += Leave(T->nextSibling);   
      res += Leave(T->firstChild);
    }

    return res;
}
```
##  2. <a name='DC07PE17'></a> DC07PE17 求以孩子兄弟链表表示的树的度 
```C
int Degree(CSTree T) 
{  
  if(T==NULL)
    return 0;
  
  CSTree p = T->firstChild, pN ;
  //树的度为树内各结点最大的度
  int maxDegree = 0;
  int count=0;
  while(p!=NULL)
  {
    pN = p->nextSibling;
    count = 1;
    while(pN!=NULL)
    {
      count++;
      pN = pN->nextSibling;
    }
    if(count>maxDegree)
      maxDegree = count;
    p = p->firstChild;
  }
  return maxDegree;
}
```
##  3. <a name='DC07PE22'></a> DC07PE22 计算以双亲表示法存储的树的深度
```C
int PTreeDepth(PTree T)
{
    int count, maxDep = 0;
    
    for (int i = 0; i < T.n; i++) { 
        count = 0;
        for (int j = i; j >= 0; j = T.nodes[j].parent) 
          count++; 
        if (count > maxDep) 
          maxDep = count;
    }
    return maxDep;
}
```
##  4. <a name='DC07PE24'></a> DC07PE24 计算以双亲孩子表示法存储的树的深度 
```C
int PCTreeDepth(PCTree T) 
{
    int maxDepth = 0, count;
    
    ChildNode *p = T.nodes[T.r].firstChild;
    ChildNode *pTmp;
    
    while(p!=NULL) 
    {
        pTmp = p;
        count = 0;
        while (pTmp) 
        {
            count++;//根的孩子的深度
            pTmp = T.nodes[pTmp->childIndex].firstChild;
        }
        if(maxDepth < count) 
          maxDepth = count;
        p = p->nextChild;
    }
    
    return maxDepth+1;//根的孩子的深度加1，为根的深度
}
```
##  5. <a name='DC07PE26-'></a> DC07PE26 计算以孩子-兄弟链表表示的树的深度 
```C
int TreeDepth(CSTree T)
{   
  int count, maxDepth;
  if(T==NULL)
    return 0;
  int r1=1;//根结点深度为1
  int r2=0;

  
  if(T->firstChild!=NULL)
    r1 = TreeDepth(T->firstChild)+1;
  if(T->nextSibling!=NULL)
    r2 = TreeDepth(T->nextSibling);
  return r1>r2?r1:r2;
}
```
##  6. <a name='DC07PE63'></a> DC07PE63 实现并查集带路径压缩的查找操作 
```C
int find(MFSet S, int i) 
{
    int root, tmp;
    root = i;
    
    while (S.parent[root] != -1) 
      root = S.parent[root];
    
    while (S.parent[i] != -1) //遍历查找路径
    {    
        tmp = S.parent[i];  
        S.parent[i] = root;//置查找路径上的每个结点的双亲位标值为根结点
        i = tmp;
    }  
    
    return root;
}
```
