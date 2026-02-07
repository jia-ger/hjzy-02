https://ac.nowcoder.com/acm/contest/120563/H

> 解析：平面内知道三点坐标A B C 求三点围成的三角形面积
> S=1/2*|(B-A)X(C-A)|  叉乘运算 u=B-A=(xb-xa,yb-ya) v=C-A=(x-xa,-ya) uXv=(xb-xa)*(-ya)-(yb-ya)*(x-xa)=ybxa-yaxb+(ya-yb)x

> cout<<fixed<<setprecision(10)<<((l+r)/2)<<"\n"; 保留十位小数

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
   int xa,ya,xb,yb;
   cin>>xa>>ya>>xb>>yb;
   
   itn c=xa*yb-xb*ya;
   int d=ya-yb;
   if(d==0)
   {
   	 if(ya==0&&yb==0)cout<<"no answer";
     else if(c==4||c==-4)cout<<0;
	 else cout<<"no answer";	
   }
   else
   {
   	double x=(4.00-c)/d;
   	cout<< fixed << setprecision(3)<<x;
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
