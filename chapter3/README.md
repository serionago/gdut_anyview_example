---
sort: 3
---
# 第三章
1. [DC03PE03 改写直接插入排序算法](#DC03PE03)
2. [DC03PE06 改进的冒泡排序](#DC03PE06)
3. [DC03PE23 计数排序](#DC03PE23)

##  1. <a name='DC03PE03'></a>DC03PE03 改写直接插入排序算法
```C
void InsertSort(RcdSqList &L)
{ 
  //直接插入排序，从小到大

  //在1号位到length号位都有数据，这样就有length个数据
  for(int i=2;i<L.length+1;i++)//进行length-1次插入，因为默认第一个直接成为一个有序数列
  {
    L.rcd[L.length+1].key=L.rcd[i].key;//准备将第i个数值进行插入，设置哨兵
    int j=i-1;
    while(L.rcd[L.length+1].key<L.rcd[j].key)//直到哨兵的数值大于或等于rcd[j]
    {
      L.rcd[j+1].key=L.rcd[j].key;
      j--;
    }
    L.rcd[j+1].key=L.rcd[L.length+1].key;
  }
}
```
```C
void InsertSort(RcdSqList &L)
{ 
  //直接插入排序，从小到大
  int n = L.length+1;//监视哨
  //在1号位到length号位都有数据，这样就有length个数据
  for(int i=L.length-1;i>=1;i--)//进行length-1次插入，默认最后一个直接成为一个有序数列
  {
    if(L.rcd[i].key>L.rcd[i+1].key)
    {
        int j;
        L.rcd[n].key=L.rcd[i].key;//准备将第i个数值进行插入，设置哨兵
        for(j=i+1;L.rcd[j].key<L.rcd[n].key;j++)//直到哨兵的数值大于rcd[j]
            L.rcd[j-1].key=L.rcd[j].key;
        L.rcd[j-1].key=L.rcd[n].key;
    }
  }
}
```
##  2. <a name='DC03PE06'></a>DC03PE06 改进的冒泡排序
```C
void BubbleSort(RcdSqList &L) { 
/* 元素比较和交换必须调用以下比较函数和交换函数：*/
/* Status LT(RedType a, RedType b);   比较："<"  */
/* Status GT(RedType a, RedType b);   比较：">"  */
/* void Swap(RedType &a, RedType &b); 交换       */
    int i,j;
    int change=L.length;
    int tChange;//change的tmp

    i=1;
    while(i<L.length)
    {
      tChange=0;
      for(j=1;j<change;j++)//for(j=1;j<L.length-i+1;j++)
      {
        if(GT(L.rcd[j], L.rcd[j+1]))
        {
          Swap(L.rcd[j], L.rcd[j+1]);
          tChange=j;
        }
      }//执行完这个内循环后，tChange=进行最后一次交换记录(j+1)的前一个记录(j)位置
      //说明从第tChange+1一直到length的数据已经排好了
      //本来是只排好一个在change位置的数据，此时tChange=change-1。
      //如果数据比较好，会比预计排好的多，tChange就会小于change-1
      //就是默认时进行一轮内循环后排序好change-tChange=1个。
      //现在数据好一些，现在进行一轮内循环后排序好change-tChange>1个。
      i+=change-tChange;
      change=tChange;//使下一次内循环对从第1到tChange的数据进行比较、排序
    }
    
    
    //以下是优化前的冒泡排序
    /*
    int i,j;
    for(i=1;i<L.length;i++)
    {
      for(j=1;j<L.length-i+1;j++)
      {
        if(GT(L.rcd[j], L.rcd[j+1]))
        {
          Swap(L.rcd[j], L.rcd[j+1]);
        }
      }
    }
    */
}
```
##  3. <a name='DC03PE23'></a>DC03PE23 计数排序
```C
void CountSort(RcdSqList &L)  // 请自行定义计数数组c，用作排序辅助
{ 
  //条件:关键字不相同，所以c的元素不会有重复的数字
  //计数排序
  int c[L.length+1]={0};
  RcdType a[L.length+1]={0};
  
  //让你找一个记录L.rcd[i]，有几个小于L.rcd[i]的数，将L.rcd遍历就行
  for(int i=1;i<=L.length;i++)
  {
    for(int j=1;j<=L.length;j++)
    {
      if(L.rcd[i].key>L.rcd[j].key)//不用统计等于时的数据
        c[i]++;
    }
  }
  //现在已经生成了c
  //索引相同时，对于c和L.rcd两组数据，有这个关系：L.rcd[i]是第c[i]+1小的数据。
  //比如c[i]=0时，对应L.rcd[i]就是从小到大排序后的第1个数据。
  for(int i=1;i<=L.length;i++)
  {
    a[i]=L.rcd[i];
  }
  
  for(int i=1;i<=L.length;i++)
  {
    L.rcd[c[i]+1]=a[i];
  }
}
```
