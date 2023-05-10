# Data generator

- `data_gen.cpp` : 指定数据生成规则并生成数据

```cpp
#include <bits/stdc++.h>

using namespace std;
#define RAND mt19937 rng(chrono::steady_clock::now().time_since_epoch().count())
#define grand(l, r) uniform_int_distribution<int>(l,r)(rng)
#define pb push_back
#define pii pair<int,int>
char mp[1005][1005];
pii pm[1005 * 1005];
int vt[1005 * 1005];

int main() {
    RAND;

    // Write Code Here
    int cats = grand(1, 120);

    cout << cats;

    return 0;
}
```

- `sample_gen.cpp` : 样例生成

```cpp
#include <iostream>
#include <windows.h>
#include <cstring>
#include <algorithm>

using namespace std;

string dig(int x) {
    string s;
    while (x > 0) {
        s += x % 10 + '0';
        x /= 10;
    }
    reverse(s.begin(), s.end());
    return s;
}

char ch1[1000000], ch2[1000000];

int main() {
    // 更改循环获得文件数量
    for (int i = 1; i <= 20; i++) {
        // std.exe 为标程
        string s1 = "data_gen.exe > ", s2 = "std.exe < ", s3 = ".in > ";
        string r = dig(i);
        s1 += r + ".in";
        s2 += r + s3 + r + ".out";
        strcpy(ch1, s1.c_str());
        strcpy(ch2, s2.c_str());
        system(ch1);
        system(ch2);
    }
    return 0;
}
```