# djistra算法

```c++
#include<iostream>
using namespace std;
const int INF = 0x3f3f3f3f;
const int maxn = 1e8 + 10;
int G[maxn][maxn];
int d[maxn][maxn];
int n,m;
void djistra(int s){
    for(int i = 0;i < n;i++){
        d[i] = INF;
    }
    d[s] = 0;
    for(int i = 0;i < n;i++){
        itn u = -1,minn = INF;
        for(int j = 0;j < n;j++){
            if(vis[j] == false && d[j] < minn){
                minn = d[j];
                u = j;
            }
        }
        if(u == -1)return ;
        vis[u] = true;
        for(int v = 0;v < n;v++){
            if(vis[v] == false && G[u][v] != INF && d[u] + G[u][v] < d[v]){
                d[v] = d[u] + G[u][v];
            }
        }
    }
}
int main(){
    cin >> n >> m;
    for(int i = 0;i < n;i++){
        for(int i = 0;i < n;i++){
            G[i][j] = INF;
        }
    }
    for(int i = 0;i < m;i++){
        int a,b,v;
        cin >> a >> b >> v;
        G[a][b] = G[b][a] = v;
    }
    djistra(0);
    for(int i = 0;i < n;i++){
        cout << d[i] << " ";
    }
    
}
```

# prime算法

```c++
#include<iostream>
using namespace std;
const int maxn = 1e3 + 10;
const int INF = 0x3f3f3f3f;
int G[maxn][maxn];
bool vis[maxn];
int n,m;
int prime(){
    for(int i = 0 ;i < n;i++){
        d[i] = INF;
    }
    d[s] = 0;
    int ans = 0 ; // 表示最小生成树的权值
    for(int i = 0 ;i < n;i++){
        int u = -1,minn = INF;
        for(int j = 0;j < n;j++){
            if(d[j] < minn && vis[j] == false){
                u = j;
                minn = d[j];
            }
        }
        if(u == -1)return -1;
        vis[u] = true;
        ans = d[u];
        for(int v = 0;v < n;v++){
            if(vis[v] == false && G[u][v] != INF && G[u][v] < d[v]){
                d[v] = G[u][v];
            }
        }
        
    }
}
int n,m;
int main(){
    cin >> n >> m;
    for(int i = 0;i < n;i++){
        for(int j = 0; j < n;j++){
            G[i][j ] = INF;
        }
    }
    for(int i = 0;i < m;i++){
        
        int a,b,v;
        cin >> a >> b >> v;
        G[a][b] = G[b][a] = v;
        
    }
    prime();
}
```

