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


# Code for detect cycle in undirected graph using BFS :
   bool bfs(int start, vector<int> adj[], vector<bool> &visited) {
    queue<pair<int, int>> q;   // for track of parents
    q.push({start, -1}); 
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front().first;
        int parent = q.front().second;
        q.pop();

        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {  
                visited[neighbor] = true;
                q.push({neighbor, node});
            }   
            else if (neighbor != parent) {  
                return true;  
            }
        }
    }
    return false;
}

bool detectCycle(int V, vector<int> adj[]) {
    vector<bool> visited(V, false);

    for (int i = 0; i < V; i++) { 
        if (!visited[i]) {  
            if (bfs(i, adj, visited)) {
                return true;
            }
        }
    }
    return false;
}
