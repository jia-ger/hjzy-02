https://ac.nowcoder.com/acm/contest/120562/H

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
    cin >> n;
    vector<int> a(n + 1);
    for (int i = 1; i <= n; i++) cin >> a[i];
    
    unordered_map<int, int> last;
    int s= 0;  //所有以 i 为右端点的区间的不同元素个数之和     
    int sum= 0;  //所有以 i 为右端点的区间的 f 值之和          f(1,r) =diff(1,1)+diff(1,2)+...+diff(1,r) 
	//sum_f[i] = sum_f[i-1] + sum_diff[i] 
    int ans = 0;
    
    for (int i = 1; i <= n; i++) {
        int pre = last.count(a[i]) ? last[a[i]] : 0;
             
        s += i - pre;  
        sum+= s;    
//        cout<<s<<" "<<sum<<endl;
        ans += sum;
        last[a[i]] = i;
    }
    
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
