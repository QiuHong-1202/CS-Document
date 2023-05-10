# Start template
```cpp
#include <bits/stdc++.h>

using namespace std;

#define LL long long
#define debug(a) cout << #a << " " << a << endl
#define de(a) cout << a << " "
#define make_unique(x) sort((x).begin(), (x).end()); (x).erase(unique((x).begin(), (x).end()), (x).end())
#define RAND mt19937 rng(chrono::steady_clock::now().time_since_epoch().count())
#define grand(l, r) uniform_int_distribution<int>(l, r)(rng)
#define PII pair<int, int>
#define fi first
#define se second
const int maxn = 3000;
const int N = 1e6 + 7, M = N * 2;
const int inf = 0x3f3f3f3f;
const long long INF = 0xFFFFFFFFFF;
const long long mod = 1e9 + 7;

inline long long read();

void solve() {

}

int main() {
#ifdef LOCAL
    int begin_time = clock();
    freopen("in.txt", "r", stdin);
//    freopen("../output.txt", "w", stdout);
#endif

//  ios::sync_with_stdio(false); //使用read和cout时不能解除流同步
    int T = 1;
//    T = read();
    for (int cas = 1; cas <= T; cas++) {
#ifdef LOCAL
        printf("Case #%d: \n", cas);
#endif
        solve();
    }

#ifdef LOCAL
    int end_time = clock();
    printf("\nRun time: %.2lf ms\n", (double) (end_time - begin_time) / CLOCKS_PER_SEC * 1000);
#endif

    return 0;
}

inline long long read() {
    char ch_read = getchar();
    long long p_read = 1, data_read = 0;
    while (ch_read < '0' || ch_read > '9') {
        if (ch_read == '-') p_read = -1;
        ch_read = getchar();
    }
    while (ch_read >= '0' && ch_read <= '9') {
        data_read = data_read * 10 + (ch_read ^ 48);
        ch_read = getchar();
    }
    return p_read * data_read;
}
```

