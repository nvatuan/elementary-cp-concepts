# Arrays 2D - C - Truy vấn Tổng âm dương

[Về Index](index.md)

## Hint giải
Trước mắt bạn vẫn sẽ phải xây dựng mảng Prefix Sum để có thể tính tổng tiền tố (tổng từ `1 -> x`) trong `O(1)`. Sau đó bạn chỉ cần cố làm đúng theo yêu cầu của đề bài là cộng, trừ đáp án nếu `x` là chẵn hoặc lẻ rồi gán `x` cho phần nguyên của `x/2`.

Mỗi lần xử lý một truy vấn, ta liên tục chia `x` cho `2` cho đến khi nó bằng `0`, ta sẽ chia `log(x)` lần. Mỗi lần, ta tính tổng tiền tố sử dụng prefix sum trong `O(1)`.

Độ phức tạp tổng cộng sẽ là `O(Q * log(x) * 1)`, với `x` lớn nhất là `n` thì sẽ là:
`O(Q * log(N))`, nghĩa là cách làm của chúng ta sẽ hoàn thành trước thời gian yêu cầu.

## Code giải

```cpp
#include <bits/stdc++.h>
using namespace std;

// -- constant
const int SIZE = 2 * 100000 + 1;

// -- data
int n;
long long a[SIZE];
long long sum[SIZE];

// -- query
int q;
int qX;
long long qAnswer;

int main() {
    // input
    cin >> n;
    // -- array starts with 1
    for (int i = 1; i <= n; i++) cin >> a[i];

    // create prefix sum
    sum[0] = 0;
    for (int i = 1; i <= n; i++) {
        sum[i] = sum[i-1] + a[i];
    }

    // answer queries
    cin >> q;
    while (q--) {
        // reset variable
        qAnswer = 0;    // reset qAnswer;

        // input
        cin >> qX;      // get queried index
        
        // process
        while (qX > 0) {
            if (qX % 2 == 0) qAnswer += sum[qX];
            else qAnswer -= sum[qX];
            qX /= 2;
        }

        // output
        cout << qAnswer << '\n';
    }
}
```