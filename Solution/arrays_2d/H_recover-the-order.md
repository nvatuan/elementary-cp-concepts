# Arrays 2D - H - Khôi phục trật tự

[Về Index](index.md)

## Hint giải

Nhận xét 1: Giới hạn thời gian cho phép Độ phức tạp `O(N^4)`.

Nhận xét 2: Hãy thử viết một chuỗi `secret` ra giấy và tạo ra ma trận đó. Bạn sẽ nhận ra một vài tính chất của mỗi phần tử và số lượng phần tử mà nó lớn hơn.

Nhận xét 3: Nếu a > b và b > c thì a > c.


## Lời giải

Với Nhận xét 2, khôi phục Trật tự sẽ rất dễ dàng, bạn chỉ cần đếm số lượng phần tử mà một phần tử lớn hơn và sắp xếp chuỗi theo số lượng đó. Nhiệm vụ còn lại là phải tạo lại mảng `greater[][]` này sao cho đầy đủ và đếm số lượng phần tử mà phần tử `i` lớn hơn.

Xét chuỗi `4 > 3 > 2 > 1`, bạn có thể thẩy số `4` lớn hơn 3 phần tử, số `3` lớn hơn 2 phần tử, số `2` lớn hơn 1 phần tử và số `1` lớn hơn 0 phần tử.

Bài toán cũng có thể giải được ở độ phức tạp `O(N^3)` với thuật toán Floyd-Warshall.

## Code nguồn

```cpp
#include <iostream>
using namespace std;

int Greater[51][51];
int GreaterCount[51];

int n;

int ans[51];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            char c; cin >> c;
            Greater[i][j] = (c == 'Y' ? true : false);
        }
    }

    for (int round = 0; round < n; round++) {
        // a > b and b > c => a > c
        // chạy round n lần để tìm ra tất cả cặp Greater[i][j]
        for (int a = 0; a < n; a++)
        for (int b = 0; b < n; b++)
            if (Greater[a][b])
                for (int c = 0; c < n; c++) 
                    if (Greater[b][c]) 
                        Greater[a][c] = true;
    }

    for (int i = 0; i < n; i++) {
        GreaterCount[i] = 0;
        for (int j = 0; j < n; j++)
            GreaterCount[i] += (Greater[i][j] ? 1 : 0);
    }

    for (int i = 0; i < n; i++) {
        if (ans[GreaterCount[i]] != 0) {
            cout << "NO\n";
            return 0;
        } else {
            ans[GreaterCount[i]] = i+1;
        }
    }
    
    // -- possible
    cout << "YES\n";
    for (int i = n-1; i >= 0; i--) {
        cout << ans[i] << ' ';
    }
    cout << endl;
}
```