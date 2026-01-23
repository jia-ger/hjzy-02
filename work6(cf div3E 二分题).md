https://codeforces.com/contest/2051/problem/E

```c++
    #include <bits/stdc++.h>
    using namespace std;
    typedef long long ll;
    const int maxn = 2e5 + 5;
    int t, n, k;
    ll ans;
    int A[maxn], B[maxn];
     
    void cal(int x)
    {
    	int tot = n - (lower_bound(B, B + n, x) - B);//b[i]>x才能卖出去 
    	int val = n - (lower_bound(A, A + n, x) - A);
    	if(tot - val > k) return;
    	ans = max(ans, ll(tot) * ll(x));
    }
     
    int main()
    {
    	ios::sync_with_stdio(0);
    	cin.tie(0);
    	cin >> t;
    	while(t--)
    	{
    		cin >> n >> k;
    		for(int i = 0; i < n; i++)
    			cin >> A[i];
    		for(int i = 0; i < n; i++)
    			cin >> B[i];
    		sort(A, A + n);
    		sort(B, B + n);
    		ans = 0LL;
    		for(int i = 0; i < n; i++)
    		{
    			cal(A[i]);
    			cal(B[i]);
    		}
    		cout << ans << '\n';
    	}
    	return 0;
    }

```
