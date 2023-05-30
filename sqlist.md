###第2章 线性表

##线性表的两种定义

```c++
#include<iostream>
#include<cstdio>

using namespace std;

#define Maxsize 100;//线性表的最大长度
typedef struct 
{
    Elemtype data[Maxsize];//顺序表的元素
    int length;//顺序表的当前长度
}SqList;//顺序表的类型定义




```

```c++
#include<iostream>
#include<cstdio>

using namespace std;

#define Maxsize 100;//表长的初始定义
typedef struct 
{
    Elemtype *data;//动态分配的指针
    int Maxsize,length;//数组的最大容量和当前个数
}SeqList;
```

##顺序表的基本操作实现

```c++
//插入操作 在第i个位置插入新元素e
bool ListInsert(SqList &L,int i,Elemtype e)
{
    if(i < 1 || i > L.length+1)return false;//判断i的范围的有效性
    if(L.length >= Maxsize)return false;//判断存储空间是否已满，不能插入的情况
    for(int j=L.length;j>=i;j--)//首先是将第i个位置以后的所有元素进行后移一位
        L.data[j]=L.data[j-1];
    L.data[i-1]=e;//插入元素e
    L.length++;//线性表的长度加1
    return true;
}

//删除操作 删除第i个位置的元素

bool DeleteList(SqList &L,int i,Elemtype &e)
{
    if(i<1 || i>L.length)return false;//判断删除位置i的有效性
    e=L.data[i-1];//取值
    for(int j=i;j<L.length;j++)
    	L.data[j-1]=L.data[j-1];//前移一个单位
    L.length--;//线性表的长度减1
    return true;
}

//按值查找 返回位序

int LocateList(SqList &L,Elemtype e)
{
    int i;
    for(i=0;i<L.length;i++)
   		if(L.data[i]==e)return i+1;//记得加1哦
    return 0;
}



```

##第2章的综合应用题

```c++
//01  删除顺序表的最小值元素（假设唯一）返回被删除的值，空出的位置有最后一个元素填补，若顺序表为空 return false
bool DeleteMin(SqList &L,Elemtype &e)
{
   	if(L.length==0)return false;
    int min=L.data[0],min_pos=0;//初始定义 最小值的大小和位置
    for(int j=1;j<L.length;j++)
    {
        if(L.data[j]<min)//如果出现新的最小值，更新最小值的大小和位置
            min=l.data[j];
        	min_pos=j;
    }
    L.data[min_pos]=L.data[L.length-1];//被删除位置的元素有最后一个元素来填补
    e=min;//引用型参数返回
    L.length--;
    return true;
}


//02 逆置顺序表中的所有元素 要求空间复杂度为0(1)

bool Reverselist(SqList L)
{
    if(L.length==0)return false;//如果线性表的长度为0则返回false
    int mid =L.length/2;
    for(int i=0;i<mid;i++)
        swap(L.data[i],L.data[L.length-i-1]);//开始从起点到中点，与终点到中点的元素进行交换
    return true;
}

//03删除长度为n的线性表中所有值为x的数据元素，要求时间复杂度为o(n),空间复杂度为o(1)

void Delete_x(SqList &L,Elemtype x)
{
    int k=0;//记录线性表中x的个数
    for(int i=0;i<L.length;i++)
    {
        if(L.data[i]==x)//如果当前值为x则k++
        {
            k++;
        }else //如果当前值不是x那么就让当前元素前移k个单位
        {
           	L.data[j-k]=L.data[j];
        }
    }
    
    L.length-=k;//最后让线性表的长度减k
}

//04  从有序的顺序表中删除值在s与t之间的数据元素(s<t)，当s或t不合理或者顺序表为空时，返回错误信息并退出

bool Delete_s_t(SqList &L,int s,int t)
{
    if(s>=t || !L.length )return false;//当s,t不满足条件或者线性表的长度为空时返回false
    int k=0;//记录满足要求的数据元素个数
    int i=0;//
    while(i<L.length)
    {
        if(L.data[i]>=s&&L.data[i]<=j)//满足要求时k++
        {
            k++;
        }else//不满足要求时候,前移k个单位
        {
            L.data[i-k]=L.data[i];
        }
        
        i++;
    }
    
    L.length-=k;//线性表的长度减k
    return true;
}

//05 上一题的有序变为无序 其他不变，所以合格问题的算法并不改变写法

bool Delete_s_t(SqList &L,int s,int t)
{
    if(s>=t || !L.length )return false;//当s,t不满足条件或者线性表的长度为空时返回false
    int k=0;//记录满足要求的数据元素个数
    int i=0;//
    while(i<L.length)
    {
        if(L.data[i]>=s&&L.data[i]<=j)//满足要求时k++
        {
            k++;
        }else//不满足要求时候,前移k个单位
        {
            L.data[i-k]=L.data[i];
        }
        
        i++;
    }
    
    L.length-=k;//线性表的长度减k
    return true;
}

//06 从有序表删除重复值，使得所有元素都不重复

bool Deletesame(SqList &L)
{
    if(!L.length)return false;//如果线性表的长度为0则返回false
   int i,j;
    for(i=0,j=1;j<L.length;j++)
    {
        if(L.data[i]!=L.data[j])//将第一个元素作为不重复的第一个元素，如果后面的元素不重复那么就让填充至第一个元素的下一个位置
        {
            L.data[++i]=L.data[j];
        }
    }
    L.length=i+1;
    return true;
}


//07 将两个有序的顺序表合并成为一个有序的线性表

bool MergeList(SqList L1,SqList L2,SqList L3)
{
    int i,j,k;
    i=0,j=0,k=0;
    while(i<L1.length && j<L2.length)//两个顺序表的遍历
    {
        if(L1.data[i]<L2.data[j])//较小值先入列
        {
            L3.data[k++]=L1.data[i++];
        }else 
        {
            L3.data[k++]=L2.data[j++];
        }
    }
    
    while(i<L1.length)L3.data[k++]=L1.data[i++];//对L1进行扫尾
    while(j,L2.length)L3.data[k++]=L2.data[j++];//对L2进行扫尾
    L3.length = k;//L3长度进行修改
    return true;
}


//08一维数组A[m+n],一次存放两个线性表am,bn,编写一个函数将其变成bn,am

void Reverse(SqList & L ,int l,int r)//基本的逆置函数
{
    int i=l,mid=r-l+/2;
    for(i;i<mid;i++)
    {
        swap(L.data[i],L.data[L.length - i-1]);
    }
}

bool Change(SqList &L,int m,int n)//三部逆置 AB -> A-B -> A-B- -> BA
{
    Reverse(L,0,m-1);
    Reverse(L,m,m+n-1);
    Reverse(L,0,m=n-1);
}

```

