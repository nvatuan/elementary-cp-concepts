# Arrays 2D - A - In tổng cộng dồn

[Về Index](index.md)

## Code nguồn

```cpp
#include <bits/stdc++.h>
using namespace std;

int n;
int a[100001];
int prefix[100001];

int main() {
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++) prefix[i] = prefix[i-1] + a[i];
    for (int i = 1; i <= n; i++) printf("%d ", prefix[i]);
    printf("\n");
}
```
