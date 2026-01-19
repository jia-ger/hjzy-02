> https://codeforces.com/contest/2191/problem/D1

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



void solve()
{
  itn n;cin>>n;
  string s;cin>>s;
  int cnt=0,ans=-1;
  for(int i=n-1;i>=0;i--)
  {
  	if(s[i]=='(')cnt++;
  	else {
  		if(cnt>=2)//一个(用来当t与s不相等的一项 另一个用来去除因为整体上少了一个) 必然要删除一个(  
  		{
  		  ans=n-2;
		  break;		
		}
	  }
  }
  cout<<ans<<endl;
  
}



signed main(){
   cin.tie(0)->sync_with_stdio(0);	 
   int T=1; 

   cin>>T;
   
  
   while(T--)solve();
   
    return 0;
}

```
