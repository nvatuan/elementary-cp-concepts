# Greedy - B - Sửa điểm

[Về Index](index.md)

## Hint giải
Ở đây là một dạng bài tối đa hóa tổng các phần tử được nhắc đến ở [trang chính của Giải thuật tham lam](../../BasicAlgorithm/Greedy.md#2-tổng-lớn-nhất-của-một-chuỗi-số) nhưng có một sửa đổi là bạn có thể sửa giá trị của một phần tử. Thay vì sửa điểm, ta có thể thêm vào ngay sau danh sách điểm đó một phần tử là `10.0` điểm. Lúc này danh sách điểm sẽ có `N+1` phần tử, ta chọn ra `N` phần tử sao cho tổng nó là lớn nhất.

Tiêu chí Tham lam ở đây là gì? Chúng ta quan trọng số điểm thì nếu sửa một con điểm, ta phải sửa nó lên Cao nhất có thể phải không? Đây chính là tiêu chí tham lam và lý do cho việc thêm điểm `10.0` vào danh sách như ở trên.

Vậy, khi sửa một điểm ta sẽ sửa nó thành `10.0`. Việc còn lại là phải sửa con điểm nào. Nếu bạn nhớ lại điều mình nói ở đoạn đầu tiên, ta chọn `N` phần tử trong danh sách `N+1` phần tử đó thì phần tử nào đã bị bỏ ra ngoài? Phần tử đó là phần tử thế nào?


## Lời giải

Chúng ta sẽ chọn phần tử có giá trị nhỏ nhất trong danh sách điểm và sửa nó thành `10.0`. Nếu chúng ta chọn con điểm có giá trị cao hơn để sửa thì chắc chắn sẽ không tối ưu. Ví dụ như `{1.0, 2.0, 3.0}` và bạn sửa điểm `2.0` thành `10.0`, bạn thấy điểm tăng lên là `8.0` trong khi sửa điểm `1.0` lại tăng lên `9.0`. Ví dụ này cho số điểm mà cách `10.0` càng xa thì nó sẽ càng tốt.

Vậy giải thuật chỉ là tìm phần tử nhỏ nhất, đổi nó thành `10.0` và tính tổng.

## Code giải

```cpp
#include <iostream>
using namespace std;

int n;

int minInd = 0;
double a[100001];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
        if (a[minInd] > a[i]) minInd = i;
    }

    a[minInd] = 10.0;
    double sum = 0.0;
    for (int i = 0; i < n; i++) sum += a[i];
    
    printf("%.6f\n", sum);
}
```