> https://codeforces.com/problemset/problem/2147/D

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


//先把奇数的出现次数统计一下 偶数肯定会被他们先后平均用完 所以肯定先轮流用奇数 使奇数变成偶数 
void solve()
{
  int n;cin>>n;
  map<int,int>mp; 
  vector<PII>a;
  int sum=0;
  for(itn i=0;i<n;i++)
  {
  	itn x;
  	cin>>x;
  	sum+=x/2;
  	mp[x]++;
  }
  for(auto i:mp)
  {
  	if(i.first%2)a.push_back(i);
  }
  sort(a.begin(),a.end(),[&](PII pa,PII pb){
  	return pa.second>pb.second;
  });
  
  int ans1=0,ans2=0;
  for(int i=0;i<a.size();i++)
  {
    if(i%2==0)ans1+=a[i].second;
	else ans2+=a[i].second;	
  } 
  cout<<ans1+sum<<" "<<ans2+sum<<endl;
}



signed main(){
   cin.tie(0)->sync_with_stdio(0);	 
   int T=1; 

   cin>>T;
   
  
   while(T--)solve();
   
    return 0;
}
```
