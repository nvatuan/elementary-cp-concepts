# Arrays 2D - G - Sàn nhảy

[Về Index](index.md)

## Hint giải

Nếu có một cách để ghi lại thời điểm chúng ta đến một ô, thì khi đến ô đó lần kế tiếp, ta có thể lấy thời gian hiện tại so với thời gian đến ô đó chính là độ dài của vòng lặp.

## Lời giải

Chúng ta sẽ sử dụng một biến đếm như là một đồng hồ đếm giờ. Cứ mỗi lần đi một ô, ta sẽ tăng đồng hồ lên 1 giây.
Sau đó, ta sẽ sử dụng một mảng 2 chiều và đánh dấu những ô chúng ta đã đến bằng số trên đồng hồ đếm giờ đó. Nếu chúng ta lặp lại thì lấy giờ trên đồng hồ trừ cho giờ ghi trên mảng 2 chiều đó, chúng ta sẽ có độ dài vòng lặp.

Việc còn lại là chúng ta phải xử lý con số trên sàn nhảy sao cho nó thành một hướng đi trên ma trận 2D. Chúng ta có thể sử dụng sức mạnh của câu lệnh `switch case` và một `struct` chứa tọa độ `X, Y`.


## Code nguồn

```cpp
#include <iostream>
using namespace std;

struct XY {
    int X, Y;
    XY () { X = 0; Y = 0; }
    XY (int x, int y) { X = x; Y = y; }
};

XY genDirection(int x) {
    switch (x) {
        case 1:
            return XY(1, -1);
        case 2:
            return XY(1, 0);
        case 3:
            return XY(1, 1);
        case 4:
            return XY(0, -1);
        case 5:
            return XY(0, 0);
        case 6:
            return XY(0, 1);
        case 7:
            return XY(-1, -1);
        case 8:
            return XY(-1, 0);
        case 9:
            return XY(-1, 1);
    }
}

int n, m;
int direction[1001][1001];
int visited[1001][1001];

XY pos;

bool inFloor(XY coord) {
    return (
        1 <= coord.X and coord.X <= n
            and
        1 <= coord.Y and coord.Y <= m
    );
}

int main() {
    // --
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++) {
            cin >> direction[i][j];
        }
    cin >> pos.X >> pos.Y;
    // --
    int turn = 1;
    while (inFloor(pos)) {
        if (visited[pos.X][pos.Y] != 0) {
            cout << turn - visited[pos.X][pos.Y] << endl;
            return 0;
        }
        visited[pos.X][pos.Y] = turn;
        turn++;

        XY dirc = genDirection(direction[pos.X][pos.Y]);
        pos.X += dirc.X;
        pos.Y += dirc.Y;
    }
    cout << -1 << endl;
}
```