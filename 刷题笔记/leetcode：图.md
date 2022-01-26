# leetcode：图

## 判断有向图是否有环：

### 802.找到最终安全状态

题干：

在有向图中，以某个节点为起始节点，从该点出发，每一步沿着图中的一条有向边行走。如果到达的节点是终点（即它没有连出的有向边），则停止。

对于一个起始节点，如果从该节点出发，无论每一步选择沿哪条有向边行走，最后必然在有限步内到达终点，则将该起始节点称作是 安全 的。

返回一个由图中所有安全的起始节点组成的数组作为答案。答案数组中的元素应当按 升序 排列。

该有向图有 n 个节点，按 0 到 n - 1 编号，其中 n 是 graph 的节点数。图以下述形式给出：graph[i] 是编号 j 节点的一个列表，满足 (i, j) 是图的一条有向边。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-eventual-safe-states
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

```c++
输入：graph = [[1,2],[2,3],[5],[0],[5],[],[]]
输出：[2,4,5,6]
解释：示意图如上。
```

**本质上图中不在环中的结点就是安全的。**

#### 方法一：深度优先搜索+三色标记法

根据题意，若起始节点位于一个环内，或者能到达一个环，则该节点不是安全的。否则，该节点是安全的。

我们可以使用深度优先搜索来找环，并在深度优先搜索时，用三种颜色对节点进行标记，标记的规则如下：

白色（用 00 表示）：该节点尚未被访问；
灰色（用 11 表示）：该节点位于递归栈中，或者在某个环上；
黑色（用 22 表示）：该节点搜索完毕，是一个安全节点。
当我们首次访问一个节点时，将其标记为灰色，并继续搜索与其相连的节点。

如果在搜索过程中遇到了一个灰色节点，则说明找到了一个环，此时退出搜索，栈中的节点仍保持为灰色，这一做法可以将「找到了环」这一信息传递到栈中的所有节点上。

如果搜索过程中没有遇到灰色节点，则说明没有遇到环，那么递归返回前，我们将其标记由灰色改为黑色，即表示它是一个安全的节点。

```c++
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>> &graph) {
        int n = graph.size();
        vector<int> color(n);

        function<bool(int)> safe = [&](int x) {
            if (color[x] > 0) {
                return color[x] == 2;
            }
            color[x] = 1;
            for (int y : graph[x]) {
                if (!safe(y)) {
                    return false;
                }
            }
            color[x] = 2;
            return true;
        };

        vector<int> ans;
        for (int i = 0; i < n; ++i) {
            if (safe(i)) {
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```

自己模仿其写的代码：

```c++
class Solution {
public:
    int n;
    vector<int> ans;
    int color[10001]={0};
    bool safe(vector<vector<int>> &graph,int u){
        if(color[u]>0){
            return color[u]==2;
        }
        color[u]=1;
        for(int i=0;i<graph[u].size();i++){
            if(!safe(graph,graph[u][i])) return false;
        }
        color[u]=2;
        return true;
    }
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        n=graph.size();
        for(int i=0;i<n;i++){
            if(safe(graph,i)){
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```

注意： vector在函数之中传递一定要用引用来实现，否则将会造成莫名的错误和超时。

c++ 11中循环的新的使用技巧：

```c++
for(auto y:graph[u]){
            if(!safe(graph,y)) return false;
        }
//原来的循环，可以用这种简单形式代替
```

注意： 二分图问题也是用深度优先搜索和着色方法解决。（886. 可能的二分法）

### 785. 判断二分图

题目：二分图 定义：如果能将一个图的节点集合分割成两个独立的子集 A 和 B ，并使图中的每一条边的两个节点一个来自 A 集合，一个来自 B 集合，就将这个图称为 二分图 。

如果图是二分图，返回 true ；否则，返回 false 。

输入：graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
输出：false
解释：不能将节点分割成两个独立的子集，以使每条边都连通一个子集中的一个节点与另一个子集中的一个节点。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/is-graph-bipartite

利用**深度优先搜索思想和染色法**：

1. 先建立邻接表；
2. 判断每个节点，能否构成二分图；
3. 使用color对节点进行标记，未染色为0, 染色的分成2种, 1/-1；

```c++
class Solution {
public:
    vector<int> color;
    bool DFS(vector<vector<int>>& graph,int u,int c){
        color[u]=c;
        for(auto v:graph[u]){
            if(color[v]==c) return false;
            if(color[v]==0&&!DFS(graph,v,-c))
                return false;
        }
        return true;
    }
    bool isBipartite(vector<vector<int>>& graph) {
        int n=graph.size();
        color=vector<int> (n,0);
        for(int i=0;i<n;i++){
            if(color[i]==0&&DFS(graph,i,1)==false)
                return false;
        }
        return true;
    }
};
```

