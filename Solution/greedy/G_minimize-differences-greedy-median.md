# Greedy - G - Tối thiểu hóa Chênh lệch

[Về Index](index.md)

## Hint giải
Sắp xếp lại chuỗi số là bước đầu tiên. Sau đó, hãy thử cho `k` tăng từ từ và theo dõi Tổng Chênh lệch thay đổi như thế nào. Có bao nhiêu phần tử nằm dưới vạch `k` và có bao nhiêu nằm trên.

## Lời giải
Xét `N` là số lẻ. Lựa chọn tốt nhất là `k` phải là [Số trung vị](https://vi.wikipedia.org/wiki/S%E1%BB%91_trung_v%E1%BB%8B) của chuỗi số. Bởi vì khi `k` nhỏ hơn giá trị của `Số trung vị` và tăng dần, tổng chênh lệch sẽ tăng dần, ngược lại, khi `k` lớn hơn giá trị của `Số trung vị` và giảm dần, tổng chênh lệch sẽ giảm dần.

Nếu `N` là số chẵn thì `Số trung vị` nào cũng cho ra kết quả tối ưu cả.

## Code giải
```cpp
#include <iostream>
#include <algorithm>
#include <climits>
using namespace std;

int n;
long long a[100001];

void input() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];
}

long long diff = LLONG_MAX;
void process() {
    sort(a, a + n);

    // n = 6 => (n-1)/2 = 2  [0 1 _2 3_ 4 5 6]
    //          (n/2)   = 3
    // n = 5 => (n-1)/2 = 2  [0 1 _2_ 3 4]
    //           n/2    = 2
    for (int median = (n-1)/2; median <= n/2; median++) {
        long long currentDiff = 0;
        for (int i = 0; i < n; i++) {
            currentDiff += abs(a[i] - a[median]);
        }
        diff = min(currentDiff, diff);
    }
}

void output() {
    cout << diff << endl;
}

int main() {
    input();
    process();
    output();
}
```