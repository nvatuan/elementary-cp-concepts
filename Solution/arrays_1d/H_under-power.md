# Arrays 1D - H - Dưới quyền điều hành

[Về Index](index.md)

## Hint giải

Khai báo một mảng `boss[]` mà `boss[i]` là mã của nhân viên là cấp trên trực tiếp điều hành nhân viên có mã số là chỉ số `i`.
Nếu như một nhân viên không có cấp trên thì giá trị `boss[]` của họ là một giá trị đặc biệt (ví dụ như -1). 
Nếu gặp giá trị này, chúng ta sẽ `return NO`, vì chúng ta biết là họ không có cấp trên.

Cấp trên của cấp trên của cấp trên của ... của `x` lúc này sẽ là: `boss[boss[boss[...boss[x]...]]]`.


## Lời giải

 Để thuận tiện cho việc cài đặt thuật toán (hay là việc code), chúng ta khai báo một biến `sep` sẽ bằng `boss[x]`.
Sau đó, sẽ chỉ có thể có hai trường hợp:
- `sep` vẫn có cấp trên, tức là `boss[sep] != -1` (-1 là giá trị đặc biệt chúng ta gán từ trước)
- `sep` không có cấp trên, tức là `boss[sep] == -1`

Chúng ta sẽ liên tục đi lên chuỗi cấp trên của cấp trên đó, liên tục check nếu `sep` có bằng `y` không, nếu có chúng ta sẽ in ra `YES` và dừng truy vấn lên nữa.
Nếu không phải, chúng ta chỉ dừng khi `sep` không còn cấp trên, lúc này chúng ta sẽ in ra `NO`.


## Code nguồn

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 1000;

int n, m;
int boss[MAX_SIZE + 1];

int q;
int x[MAX_SIZE + 1];
int y[MAX_SIZE + 1];

void input() {
    cin >> n;
    cin >> m;
    for (int i = 0; i < m; i++) {
        int a, b;
        cin >> a >> b;
        boss[a] = b;
    }
    cin >> q;
    for (int i = 0; i < q; i++) {
        cin >> x[i] >> y[i];
    }
}

bool ans[MAX_SIZE + 1];
void process() {
    for (int i = 0; i < q; i++) {
        // tra loi x[i] co duoi truong y[i] khong
        int xet = boss[x[i]];
        while (true) {
            if (xet == y[i]) {
                ans[i] = true;  // YES
                break;
            }
            if (xet == 0) {
                ans[i] = false; // NO
                break;
            }
            xet = boss[xet];
        }
    }
}

void output() {
    for (int i = 0; i < q; i++)
        if (ans[i] == true) cout << "YES" << '\n';
        else cout << "NO" << '\n';
}


int main() {
    input();
    process();
    output();
    for (int i = 1; i <= n; i++)
        cout << boss[i] << ' ';
}
```