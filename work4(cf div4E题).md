https://codeforces.com/contest/2185/problem/E


首先考虑一个事情：如果一个机器人初始位置在 x，某一时刻向左走到了 y，那么 [y,x] 之间的所有位置一定都被走过了，这是因为机器人的步长为 1，只能一步一步走回来，右侧同理。于是我们可以递推前缀最大值求出 l,r 数组，l 
i​  表示在 i 时刻，机器人向左最远走过的距离，ri​ 同理，并且这个 l i​ 和 ri​ 对于所有机器人都是适用的。
由于这道题 n,m 都非常大，所以我们考虑两种方法求答案。
第一种，枚举所有机器人并计算每个机器人第一次死亡的时间。
第二种，枚举所有操作并计算有多少个机器人在这次操作死了。但是第二种看起来就是不太可做的样子，于是我们考虑第一种。
挖掘 l,r 数组的性质，发现他们都是递增的，因为机器人的最大活动范围肯定是越来越大的。
于是我们枚举所有机器人，通过二分找到当前机器人两侧离它最近的尖刺，然后再对 l 或 r 数组进行一次二分找到该机器人第一次到达这个尖刺的位置。
左右两侧的两个尖刺取最小值就是该机器人第一次死亡的位置，这个用一个数组存起来然后再从小到大枚举时间就可以得到答案了。

时间复杂度 O(nlogn)。一定不要忘了多测清空。
```c++
//code by xxxalq
#include<bits/stdc++.h>
#define int long long
using namespace std;

const int maxn=200003,inf=2e9;

int T=1,n,ans,L[maxn],R[maxn],m,k,cnt[maxn],a[maxn];

vector<int>vec;

void solve(int pos){
    int res=k+1;
    int p=*lower_bound(vec.begin(),vec.end(),pos);
    int l=1,r=k,mid;
    while(l<r){
        mid=(l+r)/2;
        if(pos+R[mid]>=p){
            r=mid;
        }else{
            l=mid+1;
        }
    }
    if(pos+R[l]==p){
        res=min(res,l);
    }
    p=*(upper_bound(vec.begin(),vec.end(),pos)-1);
    l=1,r=k;
    while(l<r){
        mid=(l+r)/2;
        if(pos-L[mid]<=p){
            r=mid;
        }else{
            l=mid+1;
        }
    }
    if(pos-L[l]==p){
        res=min(res,l);
    }
    cnt[res]++;
    return;
}

signed main(){
    ios::sync_with_stdio(0);
    cin.tie(0);
    cin>>T;
    while(T--){
        ans=0;
        vec.clear();
        cin>>n>>m>>k;
        for(int i=1;i<=k+1;i++){
            cnt[i]=0;
        }
        vec.push_back(inf);
        vec.push_back(-inf);
        for(int i=1;i<=n;i++){
            cin>>a[i];
        }
        while(m--){
            int x;
            cin>>x;
            vec.push_back(x);
        }
        sort(vec.begin(),vec.end());
        int x=0;
        for(int i=1;i<=k;i++){
            char ch;
            cin>>ch;
            x+=((ch=='R')?1:-1);
            L[i]=max(L[i-1],-x);
            R[i]=max(R[i-1],x);
        }
        for(int i=1;i<=n;i++){
            solve(a[i]);
        }
        for(int i=1;i<=k;i++){
            n-=cnt[i];
            cout<<n<<' ';
        }
        cout<<'\n';
    }
    return 0;
}

```
