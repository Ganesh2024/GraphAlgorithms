# GraphAlgos

### 1) Graph Traversals

#### 1.1) BFS

```C++
vector<int> bfsOfGraph(int v, vector<int> adj[]) {
    // Code here
    vector<int> bfs;
    int vis[v]={0};
    queue<int> q;
    q.push(0); //starting node
    vis[0]=1;
    while(q.size()){
        int p = q.front();
        bfs.push_back(p);
        q.pop();
        for(auto it:adj[p]){
            if(!vis[it]){
                vis[it]=1;
                q.push(it);
            }
        }
    }
    return bfs;
}

```

#### 1.2) DFS
```C++

typedef vector<int> vi;
vi dfsv;

void dfs(int pnode,vi& vis,vi adj[]){
    vis[pnode]=1;
    dfsv.push_back(pnode);
    for(auto it:adj[pnode]){
        if(!vis[it])dfs(it,vis,adj);
    }
}

vector<int> dfsOfGraph(int v, vector<int> adj[]) {
    // Code here
    vi vis(v,0);
    for(int i=0;i<v;i++){ //to traverse connected components also
        if(!vis[i])dfs(i,vis,adj);
    }
    return dfsv;
}
```

#### 1.3) Cycle Detection of Undirected Graph Using BFS
#### 1.4) Cycle Detection of Undirected Graph Using DFS

### 2) TopoSort

#### 2.1) Topological Sort using DFS
#### 2.2) Topological Sort using BFS(Khan's Algorithm)
#### 2.3) Cycle Detection of Directed Graph using TopoSort

### 3) Shortest Path Algorithms

#### 3.1) Dijkstra
#### 3.2) Bellman-Ford
#### 3.3) Floyd-Warshall




