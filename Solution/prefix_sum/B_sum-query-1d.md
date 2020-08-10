# Arrays 2D - B - Truy vấn Tổng 1D

[Về Index](index.md)

## Hint giải
Đây là bài ứng dụng cho Prefix Sum.

Với bài toán này, `Time Limit Exceeded` thường xảy ra nhất.

Bạn phải trả lời `Q` truy vấn, khi bạn sử dụng một vòng for để trả lời cho một truy vấn, nghĩa là một truy vấn của bạn có độ phức tạp là `O(R - L + 1)` vì nó duyệt qua số lượng phần tử trong `[L, R]` của mỗi truy vấn. Thông thường cách làm này sẽ khiến giải pháp/thuật toán của bạn chạy quá lâu và bị xét là `Time Limit Exceeded`.

Bằng cách sử dụng công thức tính tổng một đoạn của Prefix Sum, bạn đã giảm độ phức tạp của một truy vấn xuống `O(1)`.

## Lời giải
Hãy sử dụng công thức tính Tổng của một đoạn từ `[L, R]` của Prefix Sum ở [phần Công dụng](../../BasicDataStructure/PrefixSum.md#công-dụng).

## Code nguồn

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, q;
int a[100001];
int prefix[100001];

int main() {
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++) prefix[i] = prefix[i-1] + a[i];

    cin >> q;
    for (int l, r; q; q--) {
        scanf("%d%d", &l, &r);
        printf("%d\n", prefix[r] - prefix[l-1]);
    }
}
```
