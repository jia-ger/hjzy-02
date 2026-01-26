https://codeforces.com/contest/2193/problem/F

> 思路：先统计出每一层的左右端点存起来，然后把起点终点也加进去 dp考虑转移 从上一层左端点转移或从上一层右端点转移 转移到当前层 最左端或最右端

```c++
#include <bits/stdc++.h>
using namespace std;
#define itn int
#define icn cin
#define int long long
#define endl '\n'
typedef pair<int,int> PII;
const int N=2e5+10;
const int INF=1e18;
const int mod=998244353;
//#define ll __int128


void solve()
{
        itn n,Ax, Ay, Bx, By;
        cin >> n >> Ax >> Ay >> Bx >> By;
        
        vector<int> xs(n), ys(n);
        for (int i = 0; i < n; i++) cin >> xs[i];
        for (int i = 0; i < n; i++) cin >> ys[i];
        
        // 记录每个 x 的 minY 和 maxY
        map<int, pair<int, int>> house;
        for (int i = 0; i < n; i++) {
            int x = xs[i], y = ys[i];
            if (!house.count(x)) house[x] = {y, y};
            else {
                house[x].first = min(house[x].first, y);
                house[x].second = max(house[x].second, y);
            }
        }
        
       
        vector<pair<int, pair<int, int>>> points; // (x, (low, high))
        points.push_back({Ax, {Ay, Ay}}); // 起点
        for (auto& p : house) {
            points.push_back({p.first, {p.second.first, p.second.second}});
        }
        points.push_back({Bx, {By, By}}); // 终点
        
        sort(points.begin(), points.end());
        
        int m = points.size();
        vector<int> dp_low(m, LLONG_MAX / 2);
        vector<int> dp_high(m, LLONG_MAX / 2);
        
        dp_low[0] = dp_high[0] = 0;
        
        for (int i = 1; i < m; i++) {
            int x_prev = points[i-1].first;
            itn low_prev = points[i-1].second.first;
            int high_prev = points[i-1].second.second;
            itn x_curr = points[i].first;
            itn low_curr = points[i].second.first;
            itn high_curr = points[i].second.second;
            
            int dx = x_curr - x_prev;
            
            // 从 low_prev 转移
            int yp = low_prev;
            // 最终到 low_curr
            int cost_to_low = min(
                abs(yp - low_curr) + 2 * (high_curr - low_curr),
                abs(yp - high_curr) + (high_curr - low_curr)
            );
            // 最终到 high_curr
            int cost_to_high = min(
                abs(yp - low_curr) + (high_curr - low_curr),
                abs(yp - high_curr) + 2 * (high_curr - low_curr)
            );
            
            dp_low[i] = min(dp_low[i], dp_low[i-1] + dx + cost_to_low);
            dp_high[i] = min(dp_high[i], dp_low[i-1] + dx + cost_to_high);
            
            //-------------------------------------------------------------------
            
            // 从 high_prev 转移
            yp = high_prev;
            cost_to_low = min(
                abs(yp - low_curr) + 2 * (high_curr - low_curr),
                abs(yp - high_curr) + (high_curr - low_curr)
            );
            cost_to_high = min(
                abs(yp - low_curr) + (high_curr - low_curr),
                abs(yp - high_curr) + 2 * (high_curr - low_curr)
            );
            
            dp_low[i] = min(dp_low[i], dp_high[i-1] + dx + cost_to_low);
            dp_high[i] = min(dp_high[i], dp_high[i-1] + dx + cost_to_high);
        }
        
       
        int ans = min(dp_low[m-1], dp_high[m-1]);
        cout << ans << "\n";      
}


signed main() {
	cin.tie(0)->sync_with_stdio(0);
	int T=1;
	cin>>T;

	while(T--)solve();

	return 0;
}

```
