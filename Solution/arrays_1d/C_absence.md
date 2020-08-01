# Arrays 1D - C - Vắng mặt

[Về Index](index.md)

## Hint giải

Khai báo một mảng `diemDanh[]` và sử dụng chỉ số `i` như là mã số học sinh.


## Lời giải


Ban đầu, mảng `diemDanh[]` của chúng ta sẽ chứa toàn giá trị `false`, vì lớp học vừa mở cửa và không có ai trong đó cả. Sau đó, chúng ta sẽ lần lượt cho từng học sinh vào và đánh dấu là học sinh đó có mặt. Sau đó chỉ cần duyệt qua tất cả mã số học sinh, in ra các mã số học sinh mà có `diemDanh[i] == false`.

Giả sử như lớp chúng ta chỉ có 10 hoạc sinh và có các học sinh như sau đi học 11, 14, 15. Gán `diemDanh[3] = true, diemDanh[4] = true, diemDanh[7] = true;`. Sau đó, chúng ta duyệt lần lượt mã số học sinh từ 1 cho đến 10, nếu `diemDanh[mã_số_học_sinh] == false` tức là học sinh đó không có mặt.


## Code nguồn

```cpp
#include <iostream>
using namespace std;

int n, m;
int a[100001];
int diemDanh[100001];

void input() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) cin >> a[i];
}

void process() {
    for (int i = 0; i < m; i++) diemDanh[a[i]] = true;
}

void output() {
    for (int i = 1; i <= n; i++)
        if (diemDanh[i] == false)
            cout << i << " ";
    cout << "\n";
}

int main() {
    input();
    process();
    output();
}
```