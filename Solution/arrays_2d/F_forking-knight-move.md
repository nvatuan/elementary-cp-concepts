# Arrays 2D - F - Forking Knight move

[Về Index](index.md)

## Hint giải

Với bài toán này, điều khó khăn chỉ là khả năng tái hiện lại cơ chế của con mã bằng code, mọi giới hạn khác không phải là vấn đề. Để dễ dàng, chúng ta sẽ viết một hàm nhận vào một tọa độ và trả về các tọa độ có thể đi và hợp lệ của con mã.

Sau đó, ta sẽ đầu tiên sử dụng hàm để sinh ra các vị trí cần kiểm tra. Sau đó, với mỗi vị trí, ta sẽ sử dụng hàm đó và kiểm tra các tọa độ sinh ra bởi hàm đó có bao nhiêu quân đen.

## Lời giải

Dưới đây là một hàm sẽ nhận vào một tọa độ là tọa độ của con Mã và trả về một danh sách tọa độ có thể đi được:

```cpp
vector<XY> generateKnightMoves(XY toaDo) {
    vector<XY> moves;

    for (int s1 = -1; s1 <= 1; s1 += 2)
        for (int s2 = -1; s2 <= 1; s2 += 2) {
            int nextX = toaDo.X + 2*s1;
            int nextY = toaDo.Y + s2;
            if (1 <= nextX and nextX <= 8)
                if (1 <= nextY and nextY <= 8)
                    moves.push_back(XY(nextX, nextY));
        }

    for (int s1 = -1; s1 <= 1; s1 += 2)
        for (int s2 = -1; s2 <= 1; s2 += 2) {
            int nextX = toaDo.X + s1;
            int nextY = toaDo.Y + 2*s2;
            if (1 <= nextX and nextX <= 8)
                if (1 <= nextY and nextY <= 8)
                    moves.push_back(XY(nextX, nextY));
        }

    return moves;
}
```

## Code nguồn

```cpp
#include <iostream>
#include <vector>
using namespace std;

int black[10][10];

struct XY {
    int X, Y;
    XY() { X = 0; Y = 0; }
    XY(int x, int y) { X = x; Y = y; }
};

XY knight;

vector<XY> generateKnightMoves(XY toaDo) {
    vector<XY> moves;

    for (int s1 = -1; s1 <= 1; s1 += 2)
        for (int s2 = -1; s2 <= 1; s2 += 2) {
            int nextX = toaDo.X + 2*s1;
            int nextY = toaDo.Y + s2;
            if (1 <= nextX and nextX <= 8)
                if (1 <= nextY and nextY <= 8)
                    moves.push_back(XY(nextX, nextY));
        }

    for (int s1 = -1; s1 <= 1; s1 += 2)
        for (int s2 = -1; s2 <= 1; s2 += 2) {
            int nextX = toaDo.X + s1;
            int nextY = toaDo.Y + 2*s2;
            if (1 <= nextX and nextX <= 8)
                if (1 <= nextY and nextY <= 8)
                    moves.push_back(XY(nextX, nextY));
        }

    return moves;
}

int main() {
    for (int i = 1; i <= 8; i++) {
        for (int j = 1; j <= 8; j++) {
            char c; cin >> c;
            black[i][j] = (c == 'X' ? true : false);
            if (c == 'K') {
                knight.X = i;
                knight.Y = j;
            }
        }
    }

    assert(knight.X != 0 and knight.Y != 0);
    vector<XY> nextMoves = generateKnightMoves(knight);

    int ans = 0;
    for (XY move : nextMoves) {
        int blackCount = 0;
        vector<XY> attacking = generateKnightMoves(move);

        for (XY attack : attacking)
            blackCount += (black[attack.X][attack.Y] ? 1 : 0);
        
        ans += (blackCount >= 2 ? 1 : 0);
    }
    cout << ans << endl;
}
```