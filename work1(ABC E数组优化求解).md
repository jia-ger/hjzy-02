## https://atcoder.jp/contests/abc441/tasks/abc441_e

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


//问题可变成 有多少i，j 符合aj-bj>ai-bi d[i]=a[j]-b[j]  
//sum 表示：到当前位置为止，所有差值小于当前差值的计数之和。
void solve()
{
  itn n;
  string s;
  cin>>n>>s;
  
  vector<int>cnt(2*n+1);//差值 D 出现的次数 差值范围-N-N 为了下标不出现负数 映射为0-2*N 
  cnt[n]=1; 
  int sum=0,ans=0,cur=n;
  for(int i=0;i<n;i++)
  {
    if(s[i]=='A')sum+=cnt[cur],cur++;//差值+1 则sum加上差值为cur的值 
	else if(s[i]=='B')sum-=cnt[--cur];//差值-1 
	
	cnt[cur]++;
	ans+=sum;	
  } 
  cout<<ans<<endl;
}



signed main(){
   cin.tie(0)->sync_with_stdio(0);	 
   int T=1; 

//   cin>>T;
   
  
   while(T--)solve();
   
    return 0;
}

```
