# Arrays 1D - F - Truy vấn tổng 1D Easy

[Về Index](index.md)

## Lời giải O(Q*N)
Có tối đa `1000` truy vấn, mỗi truy vấn có số phần tử tối đa sẽ duyệt là `1000`. Vậy thuật toán trâu `O(Q*N)` là hoàn toàn có thể.


## Code nguồn

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, q;
int a[1001];

int l[1001], r[1001];

void input() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];
    cin >> q;
    for (int i = 0; i < q; i++) cin >> l[i] >> r[i];
}

int ans[1001];

void process() {
    for (int i = 0; i < q; i++) {
        l[i]--; r[i]--; // mang danh so tu 0
        ans[i] = 0;
        for (int j = l[i]; j <= r[i]; j++)
            ans[i] += a[j];
    }
} 

void output() {
    for (int i = 0; i < q; i++)
        cout << ans[i] << '\n';
}

int main() {
    input();
    process();
    output();
}
```