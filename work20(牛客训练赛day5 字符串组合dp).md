https://ac.nowcoder.com/acm/contest/120565/F

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
        itn n, a, b;
        cin >> n >> a >> b;
        itn ans = 0;
        if(n > 112){//留下 56+x个数字 因为56是公倍数 且长度为56n+6时 可能出现少一个8子串 多2个a子串更优 
            ans += (n / 56 - 1) * max({b * 28, a * 8, (a + b) * 7});
            n -= 56 * (n / 56 - 1);
        }
        vector<int> f(n + 1);
        for(int i = 1; i <= n; i++){
            if(i >= 2) f[i] = max(f[i], f[i - 2] + b);
            if(i >= 7) f[i] = max(f[i], f[i - 7] + a);
            if(i >= 8) f[i] = max(f[i], f[i - 8] + a + b);
        }
        ans += f[n];
        cout << ans << endl;
	  
}



signed main() {

	cin.tie(0)->sync_with_stdio(0);

	int T=1;
	cin>>T;
//   mt19937 rand(time(nullptr));
	while(T--)solve();

	return 0;
}
```
