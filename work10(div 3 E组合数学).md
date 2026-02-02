https://codeforces.com/problemset/problem/2184/E

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
//#define ll __int128

int t[N*2],n,k,x[N],m;
void solve()
{
     	m=0;
		cin>>n>>k;
		for(int i=1; i<=n; i++) cin>>x[i];
		vector<int> b;
		for(int i=1; i<=n; i++) {
			if(!t[x[i]]) b.push_back(x[i]);
			t[x[i]]++;
		}
		for(int x:b) {
			int y=k-x;
			if(y<x) continue;
			if(y==x) m+=t[x]/2;
			else if(y>=1&&y<=N) m+=min(t[x],t[y]);
		}
		cout<<m<<"\n";
		for(auto x:b) t[x]=0;  
}


signed main() {
	cin.tie(0)->sync_with_stdio(0);
	int T=1;
	cin>>T;

	while(T--)solve();

	return 0;
}

```
