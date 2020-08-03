# Greedy - G - Thu nhập thất thường

[Về Index](index.md)

## Hint giải
Hãy trả lời những câu hỏi sau:
1. Nếu như chỉ có `N = 1` thì `M` phải như thế nào so với đoạn `[L1, R1]` mới là có thể?
2. Nếu như `N > 1` thì có cách nào chuyển nó về thành `N` đoạn `[Li, Ri]` thành một đoạn thôi không?
3. Sau một số ngày thì Thu nhập ít nhất và nhiều nhất cửa hàng nọ thu về được là bao nhiêu?

## Lời giải
Ý tưởng của bài là Chúng ta sẽ theo dõi Thu nhập ít nhất mà cửa hàng thu được là bao nhiêu (`Min`) và Thu nhập nhiều nhất là bao nhiêu (`Max`), sử dụng 2 Tiêu chí tham lam cho 2 biến là `Min` và `Max`. 

`Min` sẽ bằng tổng Thu nhập tối thiểu mỗi ngày, `Max` sẽ bằng Tổng Thu nhập Tối đa mỗi ngày. Sau đó nếu `M` nằm gọn trong đoạn `[Min, Max]` thì `M` hoàn toàn là có thể.

Bài này có lẽ sẽ đơn giản và dễ nhận thấy với nhiều người, nhưng ý tưởng sử dụng một đoạn giá trị `[Lmin, Rmax]` sẽ xuất hiện rất nhiều nữa trong nhiều bài toán khác.

## Code giải
```cpp
#include <iostream>
using namespace std;

int n;
long long m;
long long L[100001], R[100001];

void input() {
    cin >> n >> m;
    for (int i = 0; i < n; i++)
        cin >> L[i] >> R[i];
}

long long Lmin, Rmax;
void process() {
    Lmin = 0; Rmax = 0;
    for (int i = 0; i < n; i++) {
        Lmin += L[i]; Rmax += R[i];
    }
}

void output() {
    cout << (Lmin <= m && m <= Rmax ? "YES\n" : "NO\n");
}

int main() {
    input();
    process();
    output();
}
```