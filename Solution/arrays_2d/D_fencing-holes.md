# Arrays 2D - D - Rào hố đất

[Về Index](index.md)

## Lời giải
Một ô có 8 ô lân cận nếu như nó không nằm trên biên của ma trận. Chúng ta chỉ cần duyệt qua tất cả ô trên ma trận và nếu nó là hố đất, ta sẽ kiểm tra 8 ô lân cận đó ô nào là ô đất thì ta sẽ thay thế nó bằng ký tự `!`, còn không chúng ta bỏ qua.

Chúng ta cần cẩn thận trường hợp truy cập ngoài biên của ma trận và không ghi `!` đè lên ô hố đất.

## Code nguồn

```cpp
#include <iostream>
using namespace std;

int n, m;
int ground[2002][2002];

const int EMPTY = 0;
const int HOLE = 1;
const int SIGN = 2;

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++) {
            char c; cin >> c;
            ground[i][j] = (c == 'O' ? HOLE : EMPTY);
        }
    
    for (int i = 1; i <= n; i++)
    for (int j = 1; j <= m; j++) 
        if (ground[i][j] == HOLE) 
            for (int x = -1; x <= 1; x++)
            for (int y = -1; y <= 1; y++)
                if (ground[i+x][j+y] == EMPTY)
                    ground[i+x][j+y] = SIGN;

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            char tile;
            switch (ground[i][j]) {
                case EMPTY:
                    tile = '#'; break;
                case HOLE:
                    tile = 'O'; break;
                case SIGN:
                    tile = '!'; break;
            }
            cout << tile;
        }
        cout << '\n';
    }
}
```
