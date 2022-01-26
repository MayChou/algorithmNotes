# 搜索专题：DFS

**leetcode113:路径和**：

关键需要两个vector变量来记录最终存放的结果。

DFS通常用递归或者用栈实现，在搜索的过程中进行判断和计算，通过DFS遍历所有顶点的核心程序实现如下：

```c++
// 有向图（邻接链表实现）
constexpr int MAX_GRAPH_SIZE = 100000;
list<int> theGraph[MAX_GRAPH_SIZE];  
int graphSize;

// 判断图中某点是否已到达
bool searched[MAX_GRAPH_SIZE];  

// 当前搜索路径
vector<int> path;               

// 处理路径的程序，这里只输出终点
void handlePath() {
    cout << path.back() << endl;
}

void search(int begin) {
    path.push_back(begin);
    searched[begin] = true;

    handlePath();
    for (auto i = theGraph[begin].begin(); i != theGraph[begin].end(); ++i) {
        if (!searched[*i]) { search(*i); }
    }
    
    path.pop_back();
}
```

### 利用DFS判断题目中是否有环

如果一个无向图中不存在环路，那么这个图就一定是一个树；如果一个有向图中不存在环路，那么这个图就是一个有向无环图。

使用DFS判断有向图中是否有环路的核心程序：

```c++
// 有向图（邻接链表实现）
constexpr int MAX_GRAPH_SIZE = 100010;
list<int> theGraph[MAX_GRAPH_SIZE];
int graphSize;

// 当前搜索路径
vector<int> path;

bool handlePath() {
    for (auto i = 0; i < path.size() - 1; i++) {
        if (path[i] == path.back()) {
            printPath(i); // 从第i个元素开始输出path，此处未给出实现
            return true;
        }
    }
    return false;
}

bool search(int begin) {
    path.push_back(begin);

    if (handlePath()) { return true; }
    for (auto i = theGraph[begin].begin(); i != theGraph[begin].end(); ++i) {
        if (search(*i)) { return true; }
    }

    path.pop_back();
    return false;
}
```

### 797.所有可能路径

给你一个有 n 个节点的 有向无环图（DAG），请你找出所有从节点 0 到节点 n-1 的路径并输出（不要求按特定顺序）

 graph[i] 是一个从节点 i 可以访问的所有节点的列表（即从节点 i 到节点 graph[i][j]存在一条有向边）。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/all-paths-from-source-to-target输入：graph = [[1,2],[3],[3],[]]
输出：[[0,1,3],[0,2,3]]
解释：有两条路径 0 -> 1 -> 3 和 0 -> 2 -> 3

代码：

利用了DFS，注意要在DFS之后进行回溯。回退到之前的状态，否则，path中将会出现端点被重复加入的情况。

```c++
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    void DFS(vector<vector<int>> graph,int u,int v){
        if(u==v){
            res.push_back(path);
            return;
        }
        //path.push_back(u);
        for(int i=0;i<graph[u].size();i++){
            int now=graph[u][i];
            path.push_back(now);
            DFS(graph,now,v);
            path.pop_back();
        }
        //path.pop_back();
        return ;
    }
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        path.push_back(0);
        DFS(graph,0,graph.size()-1);
        return res;
    }
};
```

## 回溯算法：

回溯法是暴力穷举法的一个变化形式，其主要思想是：

- 每次只构造解的一个分量，将当前已经构造的分量组成一个部分构造解；
- 如果一个部分构造解可以进一步构造（添加分量），则选择下一个分量的第一个合法选择；
- 如果无法选择下一个分量，则返回，把部分构造解的最后一个分量替换成另一个合法选择；

所有的选择和部分构造解构成了一颗**解空间树**，这棵树的根节点（第0层）表示回溯算法的初始状态，之后的每一层中，第k层表示对第k个分量所做的选择，除了子节点外的节点都是**有希望的**，而叶子节点要么是一个可行的完整解，要么是**没有希望的**死胡同解；
