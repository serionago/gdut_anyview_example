---
sort: 8
---
# 第八章
1. [DC08PE12 创建有向图的邻接数组存储结构](#DC08PE12)
2. [DC08PE15 在图G中，相对于k顶点的当前邻接顶点m，求下一个邻接顶点](#DC08PE15Gkm)
3. [DC08PE17 在图G中设置顶点v到顶点w的弧或边](#DC08PE17Gvw)
4. [DC08PE21 计算以邻接表方式存储的有向图G中某顶点的出度](#DC08PE21G)
5. [DC08PE22 计算以邻接表方式存储的有向图G中某顶点的入度](#DC08PE22G)
6. [DC08PE32 创建有向图的邻接表存储结构](#DC08PE32)
7. [DC08PE34 创建无向图的邻接表存储结构](#DC08PE34)

##  1. <a name='DC08PE12'></a>DC08PE12 创建有向图的邻接数组存储结构 
```C
Status CreateDG(MGraph &G, VexType *vexs, int n,
                           ArcInfo *arcs, int e) 
{    
  InitGraph(G, DG, n);//空图
  G.n = n;
  G.e = e;
  G.kind = DG;
  for(int i=0;i<n;i++)
  {
    G.vexs[i]=vexs[i];
  }
  
  int i,j;
  for(int k=0;k<G.e;k++)
  {
    i=LocateVex(G, arcs[k].v);
    j=LocateVex(G, arcs[k].w);
    G.arcs[i][j].adj=1;
  }
  return OK;
}
```
##  2. <a name='DC08PE15Gkm'></a>DC08PE15 在图G中，相对于k顶点的当前邻接顶点m，求下一个邻接顶点
```C
int NextAdjVex(MGraph G, int k, int m) 
{   
  //邻接数组 下一个邻接结点
  int info;
  if(G.n==0&&k==0&&m==0) 
    return 0;
  if(k<0||k>=G.n)
    return -1;
  if(G.kind==UDG||G.kind==DG)
    info = 0;
  if(G.kind==UDN||G.kind==DN)
    info = INFINITY;
    
  for(int i=m+1;i<G.n;i++)
  {
    if(G.arcs[k][i].adj!=info)
    {
      return i;
    }
  }
  return -1;
}
``` 
##  3. <a name='DC08PE17Gvw'></a>DC08PE17 在图G中设置顶点v到顶点w的弧或边 
```C
Status SetArc(MGraph &G, VexType v, VexType w, ArcCell info) 
{  
  int i,j;
  i = LocateVex(G, v);
  j = LocateVex(G, w);
  if(i<0||j<0)
    return ERROR;
  G.arcs[i][j] = info;
  G.e++;
}
```
##  4. <a name='DC08PE21G'></a>DC08PE21 计算以邻接表方式存储的有向图G中某顶点的出度 
```C
int outDegree(ALGraph G, int k) 
{  
  //邻接表，有向图，k顶点的出度
  if(k>=G.n||k<0)
    return -1;
  AdjVexNode* p = G.vexs[k].firstArc;
  int od = 0;
  while(p)
  {
    p = p->next;
    od++;
  }
  return od;
}
``` 
##  5. <a name='DC08PE22G'></a>DC08PE22 计算以邻接表方式存储的有向图G中某顶点的入度 
```C
int inDegree(ALGraph G, int k) 
{   
  //邻接表，有向图，k顶点的入度
  if(k>=G.n||k<0)
    return -1;
  AdjVexNode* p;
  int id = 0;
  for(int i=0;i<G.n;i++)
  {
    //G.vexs[i]
    p = G.vexs[i].firstArc;
    while(p)
    {
      if(p->adjvex == k)
      {
          id++;
          break;
      }
      p = p->next;
    }
  }
  return id;
}
```
##  6. <a name='DC08PE32'></a>DC08PE32 创建有向图的邻接表存储结构  
```C
Status CreateDG(ALGraph &G, VexType *vexs, int n,
                            ArcInfo *arcs, int e) 
{
  int i,j,k;
  AdjVexNodeP p;
  G.n = n;
  G.e = e;
  G.kind = DG;
  //G.vexs = (VexNode*)malloc(n*sizeof(VexNode));
  G.tags = (int*)malloc(sizeof(int) * n);
  for(int i=0;i<n;i++)
  {
    G.tags[i] = UNVISITED;
    G.vexs[i].data = vexs[i];
    G.vexs[i].firstArc = NULL;
  }
  for(int k=0;k<e;k++)
  {
    i=LocateVex(G, arcs[k].v);
    j=LocateVex(G, arcs[k].w);
    if(i<0||j<0) return ERROR;
    p = (AdjVexNode*)malloc(sizeof(AdjVexNode));
    p->adjvex = j;
    p->next = G.vexs[i].firstArc;
    G.vexs[i].firstArc = p;
  }
  return OK;
}
```
##  7. <a name='DC08PE34'></a>DC08PE34 创建无向图的邻接表存储结构 
```C
Status CreateUDG(ALGraph &G, VexType *vexs, int n,
                             ArcInfo *arcs, int e) 
{  
  int i,j,k;
  AdjVexNodeP p;
  G.n = n;
  G.e = e;
  G.kind = DG;
  //G.vexs = (VexNode*)malloc(n*sizeof(VexNode));
  G.tags = (int*)malloc(sizeof(int) * n);
  for(int i=0;i<n;i++)
  {
    G.tags[i] = UNVISITED;
    G.vexs[i].data = vexs[i];
    G.vexs[i].firstArc = NULL;
  }
  for(int k=0;k<e;k++)
  {
    i=LocateVex(G, arcs[k].v);
    j=LocateVex(G, arcs[k].w);
    if(i<0||j<0) return ERROR;
    p = (AdjVexNode*)malloc(sizeof(AdjVexNode));
    p->adjvex = j;
    p->next = G.vexs[i].firstArc;
    G.vexs[i].firstArc = p;
    
    p = (AdjVexNode*)malloc(sizeof(AdjVexNode));
    p->adjvex = i;
    p->next = G.vexs[j].firstArc;
    G.vexs[j].firstArc = p;
  }
  return OK;
}
```