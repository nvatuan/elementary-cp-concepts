# Greedy - D - ...99

[Về Index](index.md)

## Hint giải
Yêu cầu của bài toán là phải in ra một số nguyên sao cho số đó là nhỏ nhất và tổng các chữ số của nó bằng `N`. Chúng ta cũng có thể chuyển bài này về một dạng mà chúng ta đã nói đến là bài [Gàu nước](../../BasicAlgorithm/Greedy.md#1-gàu-nước). Chúng ta sẽ chuyển chúng như sau:

> Có `N` lít nước và 9 loại gàu, mỗi loại gàu có thể chứa được `{1, 2, 3, 4, 5, 6, 7, 8, 9}` lít nước. Số gàu ít nhất mà bạn cần để múc chính xác `N` lít này là bao nhiêu?

Lúc này bạn có thể sử dụng Tiêu chí tham lam giống như ở bài Gàu nước, nhưng điều này chỉ đảm bảo là số gàu nước hay số lượng chữ số của đáp án của ta là ít nhất. Bạn phải làm một vài sửa đổi để nó trở thành số nhỏ nhất. Tiêu đề của đề bài cũng là một gợi ý cho bạn.

Hãy cẩn trọng, tổng của các chữ số trong đáp án **phải bằng `N`**, khác với yêu cầu của bài `Gàu nước`.


## Lời giải
Như đề bài đã sửa đổi ở trên, ta sẽ liên tục sử dụng gàu `9 lít` để múc cho đến khi `N` nhỏ hơn `9`. Lúc này, nếu `N > 0` ta lại dùng một gàu vừa đủ để múc.

Ví dụ: `N = 32` dùng **9** => `N = 23` dùng **9** => `N = 14` dùng **9** => `N = 5` dùng **5**.

Viết các gàu đó thành một số ta có: `9995`. Đây là số có số lượng chữ số ít nhất có thể, nhưng nó chưa phải là số nhỏ nhất. Để nó thành số nhỏ nhất, ta phải chuyển chữ số `5` lên đầu tiên  `9995 => 5999`.

Vậy quy trình là gì, ta liên tục trừ `N` cho 9 và viết số `9` xuống. Nếu `N` lớn hơn 0 và nhỏ hơn 9, ta viết `N` lên đầu tiên. Điều này luôn đảm bảo số của chúng ta là số nhỏ nhất, trong tất cả các số có số lượng chữ số nhỏ nhất.


## Code giải
```cpp
#include <iostream>
using namespace std;

int main(){
	int N;
	cin >> N;
	if (N % 9) cout << N % 9;
	N /= 9;
	while(N--) cout << 9;
    cout << '\n';
}
```