https://ac.nowcoder.com/acm/contest/120565/D

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
const int MOD=1e9+7;
//#define ll __int128


void solve() {
   int n;
    cin >> n;

    vector<PII> f(n); //重量 数量 
    for (int i = 0; i < n; i++) {
        cin >> f[i].second >> f[i].first;
    }

    sort(f.begin(), f.end()); 

    priority_queue<PII, vector<PII>, greater<PII>> pq; // 重量 数量 

    for (auto &[w, c] : f) {
        if (c > 0) {
            pq.emplace(w, c);
        }
    }

    int ans = 0;

    while (pq.size() > 1 || (pq.size() == 1 && pq.top().second > 1)) {
        auto [w1, cnt1] = pq.top(); 
		pq.pop();

        if (cnt1 > 1) {
            if (cnt1 % 2 == 1) {
             
                pq.emplace(w1, 1);
                cnt1--;
            }
       
            int cnt = cnt1 / 2;
            ans = (ans + (w1 % MOD) * (cnt1 % MOD)) % MOD; 
            if (cnt > 0) {
             
                pq.emplace(2 * w1, cnt);
            }
        } else { // cnt1 == 1
            auto [w2, cnt2] = pq.top(); 
			pq.pop();
            ans = (ans + w1 % MOD + w2 % MOD) % MOD;
        
            int w= w1 + w2;
            pq.emplace(w, 1);
            if (cnt2 > 1) {
                pq.emplace(w2, cnt2 - 1);
            }
        }
    }

    cout << ans << endl;
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
