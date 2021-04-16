[<< Về trang chính](../index.md)

# Set và Map
Trọng tâm của chúng ta trong phần này là sử dụng `Set` và `Map` để tìm kiếm một phần tử, điều này chỉ làm được với biểu diễn sử dụng cấu trúc dữ liệu cây. `Set` và `Map` trong `C++` và `Java` không quá khác nhau mấy, chỉ khác về ngữ pháp.

## Mục lục

## Định nghĩa
### Set
`Set` là một tập hợp các phần tử riêng biệt, nơi mà không có hai phần tử nào trong đó là giống nhau.

Vì nó là một tập hợp nên để gom nhiều phần tử lại thì các phần tử đó phải có một điểm chung. Ví dụ như `1, 2, 3,...` đều là số nguyên thì chúng sẽ nằm trong tập hợp số nguyên. Hay `Chó, mèo, chim,...` nằm trong tập hợp thú cưng.

Cũng có ý nghĩa như trên, để sử dụng `Set`, ta cần khai báo kiểu dữ liệu của nhóm phần tử mà ta muốn nó chứa.

### Map
Trước khi đến với `Map`, ta sẽ xem xét định nghĩa của cặp phần tử `Key, Value`. Trong cặp phần tử này, phần tử đầu tiên được sử dụng để lấy về phẩn tử hai. Phần tử đầu tiên được gọi là `key` (khóa) và phần tử thứ hai được gọi là `value` (giá trị).

`Map` là một tập hợp các cặp phần tử là `key->value`, nơi mà không có hai cặp phần tử nào có `key` giống nhau.

Cái tên `Map` ở đây không có nghĩa là bản đồ mà là bắt nguồn từ một nghĩa của động từ _map_:
> Liên kết một phần tử của nhóm này với một phần tử của nhóm khác.
Chúng ta có từ _ánh xạ_ cũng có nghĩa như ở trên.

Như vậy, `Map` sẽ có công dụng nối hai phần tử của hai nhóm khác nhau lại với nhau. Hai nhóm khác nhau này cụ thể sẽ là hai tập hợp bất kỳ. Một ví dụ trong thực tế là:
- **Người->Địa chỉ nhà**, `Map` này sẽ cho ta biết địa chỉ của một người bởi vì nó liên kết nhóm **Người** với nhóm **Địa chỉ nhà**.
- **Mã số nhân viên->Tên nhân viên**, `Map` này sẽ cho ta biết tên của nhân viên nếu ta có mã số của họ. Nhóm đầu tiên là nhóm **Mã** gồm một chuỗi các ký tự hay số. Nhóm thứ hai là nhóm **Tên**, sẽ chứa tên của người.
- **Số thứ tự->Có/Không**, `Map` này sẽ cho ta biết nếu một đối tượng có số thứ tự nhất định có tồn tại/xuất hiện hay không. Ví dụ cho `Map` này là một danh sách điểm danh chẳng hạn. `Map` này sẽ nối nhóm **Số thứ tự** là tập hợp số tự nhiên, với nhóm **Có/Không** chỉ có hai phần tử là `Yes` hoặc `No`.

Vì vậy, một `Map` được định nghĩa là chứa các cặp `key, value`, với ý nghĩa rằng có một liên kết từ phần tử `key` thuộc nhóm `Key` đến phần tử `value` thuộc nhóm `Value`.

Chính vì bản chất của `Map`, để sử dụng nó ta cần phải khai báo hai kiểu dữ liệu là hai tập hợp của nhóm `Key` và nhóm `Value`.


## Các biểu diễn của Set và Map trong C++ và Java
Trong thư viện chuẩn của `C++` và `Java` đều có `Set` và `Map` của riêng mỗi ngôn ngữ. Và mỗi ngôn ngữ đều sử dụng hai cấu trúc dữ liệu để biểu diễn `Set` và `Map` đó là `Tree` (cụ thể hơn là `Balanced Tree`) và `HashTable`. Biểu diễn sử dụng cấu trúc khác nhau sẽ có đặc tính khác nhau.

### Cấu trúc Set và Map sử dụng cây (Tree)
Đây là trọng tâm của chúng ta. Phần lớn thao tác đều có độ phức tạp là `O(log N)`. Các phần tử được chứa sẽ tuân theo một trật tự nhất định, hoặc là trật tự tự nhiên của nó, hoặc là trật tự mà người dùng tự định nghĩa. Chính vì chúng có theo một trật tự mà thao tác tìm kiếm sẽ chạy trong `O(log N)` nhờ vào thuật toán Tìm kiếm nhị phân.

Để tìm kiếm một phần tử, ta cung cấp giá trị cần tìm `look` và ta sẽ tìm kiếm theo 1 trong 3 tiêu chí sau:
1. Tìm một phần tử có thứ tự lớn nhất nhưng có giá trị nhỏ hơn `value`.
2. Tìm một phần tử có giá trị bằng `value`.
3. Tìm một phần tử có thứ tự nhỏ nhất nhưng có giá trị lớn hơn `value`.

Trong `C++`



### Cấu trúc Set và Map sử dụng bảng băm (HashTable)
Đây còn được gọi là biểu diễn không có thứ tự (unordered) bởi vì các phần tử mà chúng chứa không theo một trật tự nào cả. Điều này khiến cho các thao tác tìm kiếm sẽ có độ phức tạp là `O(N)` (tuyến tính) nên chúng ta sẽ không đề cập về biểu diễn này.

Đổi lại, các thao tác tìm kiếm, xóa, thêm,... có độ phức tạp khấu hao (amortized complexity) là `O(1)`. Nghĩa là, phần lớn các thao tác sẽ chạy trong `O(1)`, nhanh hơn `Tree`.

> C++: `unordered_set`, `unordered_map`,...

> Java: `HashSet`, `HashMap`,...