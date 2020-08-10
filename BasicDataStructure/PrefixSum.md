[<< Về trang chính](../index.md)

# Tổng cộng dồn (Prefix Sum)

## Table of Content
* [Lý thuyết](#lý-thuyết)
    * [Định nghĩa](#định-nghĩa)
    * [Công dụng](#công-dụng)
    * [Lưu ý](#lưu-ý)
    * [Cách xây dựng](#cách-xây-dựng)
    * [Hàm ngược của hàm](#hàm-ngược-của-hàm)
* [Link Contest và Hướng dẫn giải](#link-contest-và-hướng-dẫn-giải)


## Lý thuyết

### Định nghĩa
Tổng cộng dồn (hay tổng tiền tố) của một danh sách các phần tử `x0, x1, x2, ...` đơn giản cũng là một danh sách `y0, y1, y2, ...` cùng độ dài, mà phần tử thứ `i` có giá trị bằng tổng của `x0 + x1 + ... + xi`:

    y0 = x0
    y1 = x0 + x1
    y2 = x0 + x1 + x2
    y3 = x0 + x1 + x2 + x3
    ...
    yn = x0 + x1 + x2 + x3 + ... + xn

### Công dụng
Việc đã biết trước Tổng cộng dồn của một danh sách số cho phép chúng ta nhanh chóng tính được tổng của các phần tử của mọi mảng con. Giả sử chúng ta có một danh sách phần tử `A[]` gồm `N` phần tử, và chúng ta đã tính được Tổng cộng dồn của nó là `prefixSum[]`, ta có:

    prefixSum[0]   = A[0]
    prefixSum[1]   = A[0] + A[1]
    prefixSum[2]   = A[0] + A[1] + A[2]
    prefixSum[3]   = A[0] + A[1] + A[2] + A[3]
    ...
    prefixSum[n-1] = A[0] + A[1] + A[2] + A[3] + ... + A[n-1]

Ta muốn biết tổng của `S = A[4] + A[4] + .. + A[15] + A[16]`. Chúng ta sẽ biến đổi `S` này sao cho chúng ta có thể áp dụng `prefixSum[]` để hỗ trợ. Ta có:

    S = A[4] + A[4] + .. + A[15] + A[16]
      = A[4] + A[4] + .. + A[15] + A[16] +       0       +       0       +       0       +       0
      = A[4] + A[4] + .. + A[15] + A[16] + (A[0] - A[0]) + (A[1] - A[1]) + (A[2] - A[2]) + (A[3] - A[3])
      = A[4] + A[4] + .. + A[15] + A[16] + A[0] + A[1] + A[2] + A[3] - A[0] - A[1] - A[2] - A[3]
      = A[4] + A[4] + .. + A[15] + A[16] + (A[0] + A[1] + A[2] + A[3]) - (A[0] + A[1] + A[2] + A[3])
      = (A[0] + A[1] + A[2] + A[3]) + (A[4] + .. + A[15] + A[16]) - (A[0] + A[1] + A[2] + A[3])
      = (A[0] + A[1] + A[2] + ...  + A[15] + A[16]) - (A[0] + A[1] + A[2] + A[3])
      = prefixSum[16] - prefixSum[3]

Từ ví dụ trên, ta có thể đúc kết được công thức như sau:
    
    Sum = A[L] + A[L+1] + ... + A[R-1] + A[R].
    <=> Sum = prefixSum[R] - prefixSum[L-1]


Ví dụ cụ thể:

    A[]         = 1, 4, 3, 0, -2, 3
    prefixSum[] = 1, 5, 8, 8,  6, 9
                     ^         ^
                     L         R
    Tổng của 4 + 3 + 0 + (-2) = 5
    bằng với 6 - 1 = 5, lưu ý ở prefixSum[] chúng ta phải lùi vị trí L lui một vị trí.

### Lưu ý
Vậy với `A[L] + A[L+1] + ... + A[R-1] + A[R] == prefixSum[R] - prefixSum[L-1]`, nếu `L = 0` thì sao? Lúc này, chúng ta cần truy cập phần tử `L-1` nên khiến giá trị `i` của ta là âm, có thể xảy ra lỗi thời gian chạy. Cách mà tôi hay làm là bắt đầu đếm số trong chương trình của mình từ `1`. Lúc này, `L` có giá trị nhỏ nhất là `1`, khiến `L-1 == 0`, không xảy ra lỗi nữa.

### Cách xây dựng
Chúng ta có thể xây dựng tổng cộng dồn một cách nhanh chóng, bởi vì `prefixSum[x] = prefixSum[x-1] + A[x]`, ta xây dựng nó trong độ phức tạp `O(N)`.

Giả sử ta cần đọc một danh sách `A[]` có `100` phần tử và xây dựng mảng tổng cộng dồn `prefixSum[]` cho nó:

```cpp
int A[101];
for (int i = 1; i <= 100; i++) cin >> A[i];

int prefixSum[101];
prefixSum[0] = 0;
for (int i = 1; i <= 100; i++) prefixSum[i] = prefixSum[i-1] + A[i];
```

### Hàm ngược của hàm
Tuy tên nó là Tổng cộng dồn (hay Tổng tiền tố, Prefix Sum), nhưng chúng ta vẫn có thể sử dụng mô hình này để tính giả dụ như Tích tiền tố hay Hiệu tiền tố,... hay bất kỳ phép toán nào mà có hàm ngược lại của nó. Như phép + và phép - là hai phép toán Ngược nhau. Bởi vì:

    a + b = c <=> c - b = a

Chúng ta có thể tổng quát hơn bằng cách gọi một phép toán là `f()`, phép toán đó có hàm ngược lại là `g()` khi và chỉ khi:

    f(x) = y <=> g(y) = x

Phép toán mũ là phép toán có hàm ngược lại, đó là Phép toán căn vì:

    x^2 = y <=> căn_bậc_2(y) = x
    x^a = y <=> căn_bậc_a(y) = x

Phép toán tìm min, max, gcd của hai số không có hàm ngược lại. Tuy nhiên, chúng ta vẫn có thể cài đặt Prefix Sum của chúng ta sử dụng bất kỳ phép toán nào nếu như ta không cần phải truy vấn mảng con mà là truy vấn mảng tiền tố hoặc mảng hậu tố.

    A[]         = 5 7 3 6 9 1 2
    prefixMin[] = 5 5 3 3 3 1 1

    Min của A[0], A[1], ... A[R] = prefixMin[R]


## Link Contest và Hướng dẫn giải
[Link Contest Prefix Sum](https://codeforces.com/contests/289716)
- [Link hướng dẫn giải cho contest Prefix Sum](../Solution/prefix_sum/index.md)