# Greedy - C - Đổi tiền

[Về Index](index.md)

## Hint giải & Lời giải
Đây chính là bài được nhắc đến ở [trang chính của Giải thuật tham lam](../../BasicAlgorithm/Greedy.md#3-đổi-tiền), mục đích chỉ để test code.

Tuy loại tiền xu trong bài này khác so với loại tiền xu của bài trong bài viết nhưng giải thuật Tham lam của chúng ta vẫn đúng. Lý do và để chứng minh điều này phải dính líu đến không ít toán.


## Code giải

```cpp
#include <iostream>
using namespace std;

int K;
int ans;

int main() {
    cin >> K;

    ans = 0;
    ans += (K / 20); K %= 20;
    ans += (K / 10); K %= 10;
    ans += (K / 5);  K %= 5;
    ans += K;

    cout << ans << endl;
}
```