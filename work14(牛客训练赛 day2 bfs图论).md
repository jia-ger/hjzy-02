https://ac.nowcoder.com/acm/contest/120562/J

> view::reverse 适用于支持双向遍历的容器 vector deque list map set array 不支持queue, stack, priority_queue

```c++
#include <bits/stdc++.h>
using namespace std;
#define itn int
#define icn cin
#define int long long
#define unsigned long long ull
#define endl '\n'
typedef pair<int,int> PII;
const int N=2e5+10;
const int INF=1e7;
const int MOD=998244353;
//#define ll __int128


void solve() {
  int n,m;
  cin>>n>>m;
  vector<vector<int>>g(n+1);//存图 
  vector<int>d(n+1,0);//存度数 
  for(int i=1;i<=m;i++)
  {
  	int u,v;
	  cin>>u>>v;
	  
	  g[u].push_back(v);
	  g[v].push_back(u);
	  d[u]++,d[v]++; 
  }
  
  map<int,deque<int>>mp;
  for(int i=1;i<=n;i++)
  mp[d[i]].push_back(i);//度数 下标
  
    
  vector<int>dis(n+1,1e9);
  vector<int>ans(n+1);
  for(auto &[x,q]:mp | views::reverse)//c++20特性 反向遍历 
  {
  	for(auto &i:q)
  	{
  	   if(dis[i] > 1e8) dis[i] = -1;
       ans[i] = dis[i];
       dis[i] = 0;//以他为起点	
	}
	while(q.size()){
		 auto u = q.front();
            q.pop_front();
            for(auto &v : g[u]){
                if(d[v] >= x) continue;
                if(dis[v] > dis[u] + 1){
                    dis[v] = dis[u] + 1;
                    q.push_back(v);
                }
            }
	} 
  }
  for(itn i=1;i<=n;i++)
  cout<<ans[i]<<" \n"[i==n];
}



signed main() {

	cin.tie(0)->sync_with_stdio(0);

	int T=1;
//	cin>>T;
//   mt19937 rand(time(nullptr));
	while(T--)solve();

	return 0;
}


```
