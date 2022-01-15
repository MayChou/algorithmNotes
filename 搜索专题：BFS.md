# 搜索专题：BFS

### 1. 基本格式

广度优先搜索（BFS）一般由队列实现，且总是按照层次的顺序进行遍历，其基本写法如下：

```c++
void BFS（int s){
	queue<int> q;
    q.push(s);
    while(!q.empty()){
        取出队首元素top;
        访问队首元素top;
        将队首元素出队;
        将top的下一层结点中未曾入队的结点全部入队，并且设置为已入队;
    }
}
```

BFS常用场景：矩阵块相邻块个数，岛屿数量等



### 2. 基本例题

给出一个m*n矩阵，矩阵中的元素为0或者1.称位置（x,y)与上下左右四个为hi是相邻的。如果矩阵中有若干个1是相邻的，那么称这些1构成了一个块，求矩阵中块的个数。

```c++
#include <iostream>
#include <queue>
using namespace std;

const int maxn=100;
struct node{
    int x,y;
}Node;

int n,m;
int matrix[maxn][maxn];
bool inq[maxn][maxn]={false};
int a[4]={0,0,1,-1};
int b[4]={1,-1,0,0};

bool judge(int x,int y){
    if(x>=n||x<0||y>=m||y<0){
        return false;
    }
    if(matrix[x][y]==0||inq[x][y]==true) return false;
    return true;
}

void BFS(int x,int y){
    queue<node> q;
    Node.x=x,Node.y=y;
    q.push(Node);
    inq[x][y]=true;
    while(!q.empty()){
        node top=q.front();
        q.pop();
        for(int i=0;i<4;i++){
            int newx=top.x+a[i];
            int newy=top.y+b[i];
            if(judge(newx,newy)){
                Node.x=newx,node.y=newy;
                q.push(Node);
                inq[newx][newy]=true;
            }
        }

    }
}

int main(){
    cin>>n>>m;
    for(int x=0;x<n;x++){
        for(int y=0;y<m;y++){
            cin>>matrix[x][y];
        }
    }
    int ans=0;
    for(int x=0;x<n;x++){
        for(int y=0;y<m;y++){
            if(matrix[x][y]==1&&inq[x][y]==false){
                ans++;
                BFS(x,y);
            }
        }
    }
    cout<<ans;
    return 0
}
```

**注意点：**

inq数组的含义是结点是否已经入队，而不是结点是否已经被访问。区别在于：如果设置为是否已经访问，有可能某个结点正在队列中但还未访问，会导致结点反复入队，增加计算量。

需要对队列中的元素进行修改而不仅仅是访问时：

队列中存放的元素最好不是元素本身而是元素的编号，因为STL queue的push操作只是制造了该元素的一个副本入队，因此在入队之后对原元素的修改不会影响队列之中的副本，对队列之中副本的修改也不会改变原来的元素。