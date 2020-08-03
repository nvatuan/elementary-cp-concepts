# Greedy - A - Mua xăng

[Về Index](index.md)

## Hint giải

Hãy để ý rằng đề bài yêu cầu đổ **chính xác** `N` lít. Trước khi giải bài toán chung là đổ bất kỳ một lượng nào, chúng ta hay thử giải bài toán đổ số chẵn lít trước thử xem.

Nếu `N` là 7 thì bạn hãy thử giải quyết bài toán `N = 6` trước, bởi vì để đổ 1 lít còn lại bạn chỉ có 1 lựa chọn.

Sau đó, hãy nghĩ đến việc bạn nên Tham lam theo tiêu chí nào? Chú ý rằng ở đây chúng ta quan tâm đến số tiền càng ít càng tốt, vậy cùng một số lít mà ít tiền mua hơn thì sẽ càng tốt phải không?


## Lời giải

Nếu `N` là số lẻ, chúng ta sẽ giải quyết đổ `N-1` lít trước rồi cộng giá tiền đó cho `a` bởi vì để đổ 1 lít chỉ có một lựa chọn đó thôi.

Ở đây với số lít là số chẵn và chúng ta có hai lựa chọn:

* Đổ 1 lít với giá `a` đồng
* Đổ 2 lít với giá `b` đồng

Chúng ta sẽ đổi cách viết lựa chọn lại thành:

* Đổ 2 lít với giá `2*a` đồng
* Đổ 2 lít với giá `b` đồng

Lúc này thì mọi thứ sẽ rõ ràng hơn rồi. Vì số lít là số chẵn nên chúng ta sẽ đổ `số lít / 2` lần, ta chỉ cần chọn phương án rẻ hơn là được.

Sau đó ta sẽ đổ thêm 1 lít hay không là tùy vào `N`.

## Code giải

```cpp
#include <bits/stdc++.h>
using namespace std;

long long n, a, b;

int main(){
	cin >> n;
	cin >> a >> b;
	//
	cout << (n % 2)*a + min( n/2 * (2*a) , n/2 * b );
    // n/2 => số nguyên
    // (n % 2)*a là giá đổ thêm 1 lít nữa nếu n là số lẻ
}
```