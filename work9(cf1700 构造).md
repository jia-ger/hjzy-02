https://codeforces.com/problemset/problem/2123/F

```c++
#include <bits/stdc++.h>
using namespace std;
#define itn int
#define icn cin
#define int long long
#define endl '\n'
typedef pair<int,int> PII;
const int N=2e5+10;
const int INF=1e7;
const int MOD=998244353;
//#define ll __int128

//让每个质数都拥有一个自己的集合。
//然后从后向前扫，扫到的每一个数放入它最大质因子的集合中（质数就是它本身）。
//扫完后，对于每个集合进行一个简单的位置轮转 
itn n;
vector<int> pr[N];
int ans[N];

void work(int x) {
    int ma, tmp = x;
    for(int i = 2; i * i <= x; i++) {
        if(x % i == 0) ma = i;
        while(x % i == 0) x /= i;
    }
    if(x > 1) ma = x;
    pr[ma].push_back(tmp);
    if(tmp == ma)  {
        reverse(pr[tmp].begin(), pr[tmp].end());
        for(int i = 1; i < pr[tmp].size(); i++) ans[pr[tmp][i]] = pr[tmp][i - 1];
        ans[pr[tmp][0]] = pr[tmp][pr[tmp].size() - 1]; 
    }
}
void solve() {
        cin>>n;
        for(int i = 1; i <= n; i++) ans[i] = i;
        for(int i = n; i >= 2; i--) work(i);

        for(int i = 1; i <= n; i++) cout<<ans[i]<<" \n"[i==n];
        
        for(int i = 0; i <= n; i++) pr[i].resize(0);
	   
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
