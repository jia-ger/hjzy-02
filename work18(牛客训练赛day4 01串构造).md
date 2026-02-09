https://ac.nowcoder.com/acm/contest/120564/F

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
        itn a, b;
        cin >> a >> b;
        
        string res;
        if (a > b) {
            // 用1分隔0 分成b+1段 
            int cnt = a / (b + 1);
            int rem = a % (b + 1);
            for (int i = 0; i < b + 1; ++i) {
                res += string(cnt + (i < rem ? 1 : 0), '0');
                if (i < b) res += '1';
            }
        } else if (b > a) {
            // 用0分隔1 分成a+1段 
            int cnt = b / (a + 1);
            int rem = b % (a + 1);
            for (int i = 0; i < a + 1; ++i) {
                res += string(cnt + (i < rem ? 1 : 0), '1');
                if (i < a) res += '0';
            }
        } else {
        
            for (int i = 0; i < a; ++i) {
                res += "01";
            }
        }
        
        cout << res << '\n';
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
