## Code for basic implementation of BFS:
// In question adjancey matrix or list is given

void bfs(vector<int> adj[], int v, int s) {
    vector<bool> visited(v + 1, false);
    queue<int> q;
    visited[s] = true;
    q.push(s);
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        cout << u << " ";
        for (int v : adj[u]) {
            if (!visited[v]) {
                visited[v] = true;
                q.push(v);
            }
        }
    }
}


## code for when no source is given or graph may be disconnected (similar to no of components) )

void bfsDis(vector<int>adj[], int v){
   vector<bool>visited(v+1, false);
    int cnt=0
   for(int i=0; i<v; ++i){
   if( visited[i] ==false){
    cnt++;
   bfs(adj, i , visited);
}



}
}


## convert edge list ( vector<vector<int>>& edges ) into adjacency list
 // Convert edge list to adjacency list
    for (auto& edge : edges) {
        adj[edge[0]].push_back(edge[1]);
        adj[edge[1]].push_back(edge[0]);  
    }


## Basic DFS code :
  void dfs (vector<int>adj[], int v, int s){
   vector<bool>visited(v, false);
   for(int i=0;i<v;++i){
if(visited[i]==false){
  dfsrec(adj, i, visited);
}
}
  }

void dfsrec(vector<int>adj[], int s, vector<bool> visited){
visited[s] = true;
cout<< s <<endl;

for(int u: adj[s]){
if(visited[u]==false){
   dfsrec(adj, u, visited)
}
}
}



## Cycle Detection
```
//DFS
class Solution {
  private:
    bool detect(int src,int parent, vector<vector<int>> &adj, vector<int> &vis){
        vis[src] = 1;
        for(auto it: adj[src]){
            if(it==parent) continue;
            if(vis[it]==1) return true;
            else if(detect(it,src,adj,vis)) return true;
        }
        return false;
    }
  public:
    // Function to detect cycle in an undirected graph.
    bool isCycle(vector<vector<int>>& adj) {
        int n = adj.size();
        vector<int> vis(n,0);
        for(int i=0;i<n;i++){
            if(!vis[i] && detect(i,-1, adj, vis)){
                return true;
            }
        }
        return false;
    }
};
```

```
//BFS
class Solution {
  private:
    bool detect(int src, vector<vector<int>> &adj, vector<int> &vis){
        vis[src] = 1;
        queue<pair<int,int>> q; 
        q.push({src, -1});
        while(!q.empty()){
            int node = q.front().first;
            int parent = q.front().second;
            q.pop();
            for(auto it: adj[node]){
                if(!vis[it]){
                    vis[it]=1;
                    q.push({it, node});
                } else if(parent!=it) return true;
            }
        }
        return false;
    }
  public:
    // Function to detect cycle in an undirected graph.
    bool isCycle(vector<vector<int>>& adj) {
        // Code here
        int n = adj.size();
        vector<int> vis(n,0);
        for(int i=0;i<n;i++){
            if(!vis[i] && detect(i, adj, vis)){
                return true;
            }
        }
        return false;
    }
};
```

## Number of Provinces
```
class Solution {
private:
    void dfs(int start, vector<int> &vis, vector<vector<int>> &adj){
        vis[start] = 1;
        for(auto it: adj[start]){
            if(!vis[it]){
                dfs(it, vis, adj);
            }
        }
    }
    void bfs(int start, vector<int> &vis, vector<vector<int>> &adj){
        queue<int> q;
        vis[start] = 1;
        q.push(start);
        while(!q.empty()){
            int node = q.front();
            q.pop();
            for(auto it: adj[node]){
                if(!vis[it]){
                    vis[it] = 1;
                    q.push(it);
                }
            }
        }
    }
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        vector<vector<int>> adj;
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                adj[i].emplace_back(j);
                adj[j].emplace_back(i);
            }
        }
        vector<int> vis(n,0);
        int count = 0;
        for(int i=0;i<n;i++){
            if(!vis[i]){
                count++;
                bfs(i, vis, adj);
                // dfs(i, vis, adj);
            }
        }
        return count;
    }
};
```

## Topological Sort
```
class Solution {
  private:
    void dfs(int start, vector<int> &vis, stack<int> &st, vector<vector<int>> &adj){
        vis[start]=1;
        for(auto it: adj[start]){
            if(!vis[it]){
                dfs(it, vis, st, adj);
            }
        }
        st.push(start);
    }
  public:
    // Function to return list containing vertices in Topological order.
    vector<int> topologicalSort(vector<vector<int>>& adj) {
        // Your code here
        int n = adj.size();
        vector<int> vis(n,0);
        stack<int> st;
        for(int i=0;i<n;i++){
            if(!vis[i]){
                dfs(i, vis, st, adj);
            }
        }
        vector<int> ans;
        while(!st.empty()){
            ans.push_back(st.top());
            st.pop();
        }
        return ans;
    }
};
```
## Kahn's Algorithm
```
vector<int> indegree(n,0);
for(int i=0;i<n;i++){
    for(auto it: adj[i]){
        indegree[it]++;
    }
}
queue<int> q;
for(int i=0;i<n;i++){
    if(indegree[i]==0){
        q.push(i);
    }
}
vector<int> topo;
    while(!q.empty()){
        int node = q.front();
        q.pop();
        topo.push_back(node);
        for(auto it: adj[node]){
            indegree[it]--;
            if(indegree[it]==0) q.push(it);
        }
    }
return topo;
```


