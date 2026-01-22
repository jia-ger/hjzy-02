https://codeforces.com/contest/2074/problem/E

> 思路分析：利用随机数 将三角形分成三部分随机选取一个点变成这个点，防止超时

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

int p,l,r;
void solve()
{
  cout.flush();		
  int n;cin>>n;
  if(n==3){
  	cout<<"! 1 2 3"<<endl;return;
  }	  
  l=1,r=2,p=3;
  while(1)
  {
  	cout<<"? "<<l<<" "<<r<<" "<<p<<endl;
	cout.flush();	
    int ran= rand() % 3;
        int x;
        cin >> x;
        if(x == 0) { cout << '!' << ' ' << l<< ' ' << r << ' ' << p <<endl; return; }
        if(ran== 0) l= x;
        else if(ran== 1) r = x;
        else p= x;
  }
  cout<<"! "<<l<<" "<<r<<" "<<p<<endl;
}



signed main(){
//   cin.tie(0)->sync_with_stdio(0);	 
   int T=1; 
   cin>>T;
   mt19937 rand(time(nullptr)); 
   while(T--)solve();
   
    return 0;
}
```
