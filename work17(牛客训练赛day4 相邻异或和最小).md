https://ac.nowcoder.com/acm/contest/120564/C

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
  itn n;
  cin>>n;
  int sz=1<<n;
  for(itn i=0;i<sz;i++)
  {
  	int x=i ^ (i>>1);
  	cout<<x<<" \n"[i==sz-1];
  }
  
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
