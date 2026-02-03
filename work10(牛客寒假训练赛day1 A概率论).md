https://ac.nowcoder.com/acm/contest/120561/A

> 分析：显示器之间相互独立，所以我们其实可以分别求出显示器显示出0-9每个数字的概率。假如我们有了这个概率，我们就能求出四个显示器显示出某个四位数的概率，这个概率显然是这四个显
示器分别显示其数位的概率乘积。（因为是独立事件）因此我们就可以枚举A，计算出B=C-A
则对于当前枚举的A,B，就可以计算出显示出A,B这两个四位数字的概率，那么对于当前的枚举，这两
组显示器显示出C的概率就等于：P(C)=P(A)*P(B)

```c++
#include <bits/stdc++.h>
using namespace std;
#define itn int
#define icn cin
#define int long long
#define endl '\n'
typedef pair<int,int> PII;
const int N=7;
const int INF=1e18;
const int MOD=998244353;
//#define ll __int128

const int inv100 = 828542813; 

int S[N];
void init() {
S[0] = (1 << 0) | (1 << 1) | (1 << 2) | (1 << 4) | (1 << 5) | (1 << 6);
S[1] = (1 << 2) | (1 << 5);
S[2] = (1 << 0) | (1 << 2) | (1 << 3) | (1 << 4) | (1 << 6);
S[3] = (1 << 0) | (1 << 2) | (1 << 3) | (1 << 5) | (1 << 6);
S[4] = (1 << 1) | (1 << 2) | (1 << 3) | (1 << 5);
S[5] = (1 << 0) | (1 << 1) | (1 << 3) | (1 << 5) | (1 << 6);
S[6] = (1 << 0) | (1 << 1) | (1 << 3) | (1 << 4) | (1 << 5) | (1 << 6);
S[7] = (1 << 0) | (1 << 2) | (1 << 5);
S[8] = (1 << 0) | (1 << 1) | (1 << 2) | (1 << 3) | (1 << 4) | (1 << 5) | 
(1 << 6);
S[9] = (1 << 0) | (1 << 1) | (1 << 2) | (1 << 3) | (1 << 5) | (1 << 6);
}


void solve()
{
    int C;
    cin>>C;
    vector<int> p(N);
    for(int i = 0; i < N; i++) {//每根灯管点亮的概率 
        cin >> p[i];
        p[i] = (1LL * p[i] * inv100) % MOD;
    }
    
    vector<int> digit(10, 1); // 一个显示器表示出 (0-9) 的概率
    for(int i = 0; i < 10; i++) {
        for(int j = 0; j < N; j++) {
            if(S[i] >> j & 1) {
                digit[i] *= p[j];
            } else {
                digit[i] *= (1 + MOD - p[j]);
            }
            digit[i] %= MOD;
        }
    }
    
      auto calc = [&](int x) -> int { // 求四个显示器表示出四位数 x 的概率
        if(x == 0) {
            return digit[0] * digit[0] % MOD * digit[0] % MOD * digit[0] %MOD;
        }
        int ans = 1;
        int len = 0;
        while(x > 0) {
            ans *= digit[x % 10];
            ans %= MOD;
            x /= 10;
            len++;
        }
        for(int i = 0; i < 4 - len; i++) {//前导0 
            ans = (ans * digit[0]) % MOD;
        }
        return ans;
    };
    
    int ans=0;
	for(int A = 0; A <= C; A++) {
        int B = C - A;
        ans += 1LL * calc(A) * calc(B) % MOD;
        ans %= MOD;
    }
    cout << ans << endl ;
}


signed main() {
	cin.tie(0)->sync_with_stdio(0);
	int T=1;
	cin>>T;
    init(); 
	while(T--)solve();

	return 0;
}
```
