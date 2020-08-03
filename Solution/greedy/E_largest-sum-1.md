# Greedy - E - Tổng lớn nhất 1

[Về Index](index.md)

## Hint giải
Đây là một biển đổi của bài tối đa hóa tổng các phần tử được nhắc đến ở [trang chính của Giải thuật tham lam](../../BasicAlgorithm/Greedy.md#2-tổng-lớn-nhất-của-một-chuỗi-số). Vì chúng ta tính tổng của các giá trị tuyệt đối nên chúng ta phải ưu tiên phần tử có giá trị tuyệt đối như thế nào?

Tiêu chí Tham lam ở đây là gì? 


## Lời giải
Chúng ta có thể gán các phần tử đó bằng giá trị tuyệt đối của nó rồi làm như bình thường. Sắp xếp rồi lấy tổng của `K` phần tử có giá trị lớn nhất.


## Code giải
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int n, k;
int a[200001];

int main() {
    cin >> n >> k;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
        a[i] = abs(a[i]);
    }
    sort(a, a + n);

    long long sum = 0;
    for (int i = n-1; k > 0; k--, i--) {
        sum += a[i];
    }
    cout << sum << '\n';
}
```