https://codeforces.com/contest/2193/problem/E

> 思路：先把可以一次实现的记录下来，那么其余的数就是由这些可以实现的转移过去的

```c++
#include <bits/stdc++.h>
using namespace std;
#define itn int
#define icn cin
#define int long long
#define endl '\n'
typedef pair<int,int> PII;
const int N=2e5+10;
const int INF=1e18;
const int mod=998244353;
#define ll __int128


void solve()
{
  int n;
  cin>>n;
  set<int>a;
  for(itn i=1;i<=n;i++)
  {
  	itn x;
  	cin>>x;
  	a.insert(x);
  }
  vector<int>dp(n+1,INF);
  
  for(auto i:a)
  {
  	if(i<=n)dp[i]=1;
  }
  
  for(int i=1;i<=n;i++)
  {
  	if(dp[i]==INF)continue;
  	for(auto j:a)
  	{
  	 itn x=	j*i;
  	 if(x>n)break;
  	 dp[x]=min(dp[x],dp[i]+1);
	}
  }
  for(int i=1;i<=n;i++)
  if(dp[i]==INF)cout<<-1<<" ";
  else cout<<dp[i]<<" ";
  
  cout<<endl;
}


signed main() {
	cin.tie(0)->sync_with_stdio(0);
	int T=1;
	cin>>T;

	while(T--)solve();

	return 0;
}

```
