# Graph Algorithms

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
```C++
typedef vector<int> vi;
typedef pair<int,int> pii;

bool bfs(int i,vi& vis,vi adj[]){
    queue<pii> q;
    q.push({0,-1});
    vis[i]=1;
    while(!q.empty()){
        int node=q.front().first;
        int pnode=q.front().second;
        q.pop();
        for(auto it:adj[node]){
            if(!vis[it]){
                vis[it]=1;
                bfs(it,vis,adj);
            }
            else if(pnode==it)return 1;
        }
    }
    return 0;
}

bool isCycle(int v, vector<int> adj[]) {
    // Code here
    vi vis(v,0);
    for(int i=0;i<v;i++){
        if(!vis[i] and bfs(i,vis,adj))return 1;
    }
    return 0;
}
```

#### 1.4) Cycle Detection of Undirected Graph Using DFS
```C++
typedef vector<int> vi;
bool dfs(int i,vi& vis,vi adj[]){
    vis[i]=1;
    for(auto it:adj[i]){
        if(!vis[it] and dfs(it,vis,adj))return 1;
        else if(it!=i)return 1;
    }
    return 0;
}

bool isCycle(int v, vector<int> adj[]) {
    // Code here
    vi vis(v,0);
    for(int i=0;i<v;i++){
        if(!vis[i] and dfs(i,vis,adj))return 1;
    }
    return 0;
}
```

### 2) TopoSort

#### 2.1) Topological Sort using DFS
```C++
typedef vector<int> vi;
vi topol;
stack<int>  st;

void dfs(int i,vi& vis,vi adj[]){
    vis[i]=1;
    for(auto it:adj[i]){
        if(!vis[it])dfs(it,vis,adj);
    }
    st.push(i);
}

vector<int> topoSort(int v, vector<int> adj[]){
    vi vis(v,0);
    for(int i=0;i<v;i++){
        if(!vis[i])dfs(i,vis,adj);
    }
    while(!st.empty()){
        topol.push_back(st.top());
        st.pop();
    }
    return topol;
}

```
#### 2.2) Topological Sort using BFS(Khan's Algorithm)
```C++
typedef vector<int> vi;
vi topol;

vector<int> topoSort(int v, vector<int> adj[]){
    vi inDegree(v,0);
    for(int i=0;i<v;i++){
        for(auto it:adj[i])inDegree[it]++;
    }
    queue<int> q;
    for(int i=0;i<v;i++){
        if(inDegree[i]==0)q.push(i);
    }
    while(!q.empty()){
        int node=q.front();
        q.pop();
        topol.push_back(node);
        for(auto it:adj[node]){
            inDegree[it]--;
            if(inDegree[it]==0)q.push(it);
        }
    }
    
    return topol;
}
```
#### 2.3) Cycle Detection of Directed Graph using TopoSort
```
if number of vertices == topol.size()
    return 0; //no cycle
return 1 //cycle detected
```

### 3) Shortest Path Algorithms

#### 3.1) Dijkstra
```C++
typedef pair<int,int> pii;
typedef vector<int> vi;
vector <int> dijkstra(int v, vector<vector<int>> adj[], int s)
{
    // Code here
    set<pii> st;
    vi dist(v,1e9);
    st.insert({0,s});
    dist[s]=0;
    while(!st.empty()){
        auto it = *(st.begin());
        int pnode = it.second;
        int d = it.first;
        st.erase(it);
        
        if(dist[s]<d)continue;
        for(auto it:adj[pnode]){
            
            if(d+it[1]<dist[it[0]]){
                if(dist[it[0]]!=1e9){
                    st.erase({dist[it[0]],it[0]});
                }
                dist[it[0]] = d+it[1];
                st.insert({dist[it[0]],it[1]});
            }
            
        }
    }
    return dist;
}
```
#### 3.2) Bellman-Ford
#### 3.3) Floyd-Warshall




