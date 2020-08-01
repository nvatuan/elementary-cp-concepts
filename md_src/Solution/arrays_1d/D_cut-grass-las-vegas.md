# Arrays 1D - D - Cắt cỏ Las Vegas

[Về Index](index.md)

## Lời giải


Duyệt từ vị trí đầu đến vị trí cuối, mỗi lần duyệt ta xét 3 phần tử liên tục kế tiếp có phải là `W` hay không, nếu có cứ xóa chúng. Xóa 3 ô đầu tiên ngay khi có thể là một trong những cách xóa tối ưu.


## Code giải

```cpp
#include <iostream>
using namespace std;

int n;
int grass[100001];

void input() {
    cin >> n;
    char c;
    for (int i = 0; i < n; i++) {
        cin >> c;
        if (c == 'W') grass[i] = true;
        else grass[i] = false;
    }
}

int ans = 0;
void process() {
    for (int i = 0; i+2 < n; i++) {
        if (grass[i] && grass[i+1] && grass[i+2])
            grass[i] = grass[i+1] = grass[i+2] = false; // cut grass
    }
    for (int i = 0; i < n; i++)
        ans += (grass[i] ? 1 : 0);
}

void output() {
    cout << ans << "\n";
}

int main() {
    input();
    process();
    output();
}
```