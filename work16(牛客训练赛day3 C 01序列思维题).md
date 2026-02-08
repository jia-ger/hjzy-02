https://ac.nowcoder.com/acm/contest/120563/C

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

//反向理解 如果原串某序列符合0101 那么其余序列肯定符合1010 所以只需把符合0101的全变成符合1010串即可 
int f(string s){//找最大子段和 与最小子段和 操作几次取决于里面连着的1/0最多出现几次 
    int mx=0,mn=0,now=0;
    for(int i=0;i<(int)s.size();i++){
        if(s[i]=='1')now++;
        else now--;
        if(now<0)now=0;
        mx=max(mx,now);
    }
    now=0;
    for(int i=0;i<(int)s.size();i++){
        if(s[i]=='1')now++;
        else now--;
        if(now>0)now=0;
        mn=min(mn,now);
    }
    return max(mx,abs(mn));
}
 
void solve() {

 int n,i;
    string s,t;
    cin>>n>>s;
    t="";
    for(i=0;i<n;i++){//0101...
        if((i&1)&&s[i]=='1')t+=s[i];
        if(!(i&1)&&s[i]=='0')t+=s[i];
    }
    int ans=f(t);
//    cout<<ans<<endl;
    t="";
    for(i=0;i<n;i++){//1010...
        if((i&1)&&s[i]=='0')t+=s[i];
        if(!(i&1)&&s[i]=='1')t+=s[i];
    }
    ans=min(ans,f(t));
    cout<<ans<<"\n";
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
