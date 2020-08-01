# Arrays 2D - E - Truy vấn Tổng 2D Easy

[Về Index](index.md)

## Hint giải

Rằng buộc của dữ liệu đầu vào cho phép độ phức tạp thuật toán là `O(N*M*Q)`. Bạn có thể duyệt qua mỗi phần tử trong khu vực được truy vấn để lấy đáp án mà không cần lo đến giới hạn thời gian.


## Code nguồn

```cpp
#include <iostream>
using namespace std;

int n, m;
long long a[1002][1002];
int q;

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            cin >> a[i][j];
    
    cin >> q;
    for (int x1, y1, x2, y2; q; q--) {
        cin >> x1 >> y1 >> x2 >> y2;
        
        long long ans = 0;
        for (int i = x1; i <= x2; i++)
            for (int j = y1; j <= y2; j++)
                ans += a[i][j];
        cout << ans << '\n';
    }
    
}
```
