# Arrays 1D - G - Dọn dẹp đường ray

[Về Index](index.md)

## Hint giải

Nhận xét 1: Toa đầu tiên và toa cuối cùng phải là đầu tàu.

Nhận xét 2: Từ trái sang phải, các toa thân phải được nối vào toa đầu tàu. Và từ phải sang trái, các toa thân phải được nối vào toa đầu tàu.

Nhận xét 3: Một đầu tàu có thể đi được sang trái nếu đoàn tàu ngay bên trái nó có thể được dọn dẹp. Điều đó cũng đúng với hướng còn lại.


## Lời giải O(N)


Chúng ta sẽ duyệt từ trái sang phải, và rồi từ phải sang trái. Với mỗi hướng duyệt, ta sẽ làm như sau:

- Nếu toa đầu tiên là đầu tàu, toa tàu đó sẽ được đánh dấu là `Có thể dọn`.
- Từ toa thứ hai trở đi, nếu là toa thân và được nối với toa trước nó, mà toa trước nó `Có thể dọn` thì nó cũng là `Có thể dọn`.
- Nếu toa đó là toa đầu, nếu toa trước là `Có thể dọn` thì nó cũng có thể dọn, vì nó có thể di chuyển theo hướng ngược lại hướng đang duyệt. Chúng ta có thể xem toa đầu tàu từ thứ 2 trở đi như là toa thân tàu mà được nối vào toa trước nó.

Sau khi duyệt hai hướng đó, ta sẽ duyệt qua một lần nữa, nếu có toa mà `Không thể dọn` thì nó là bất khả thi. Ngược lại là có.


## Code nguồn

```cpp
#include <iostream>
using namespace std;

int n, m;
int isHead[100001];
int connect[100001];

void input() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        char c; cin >> c;
        isHead[i] = (c == 'H' ? true : false);
    }
    cin >> m;
    for (int a, b, i = 0; i < m; i++) {
        cin >> a >> b;
        a--; b--;
        connect[a] = true;
        // khong can b.
        // connect[x] == true nghia la toa tau X va X+1 co noi voi nhau
    }
}

int clear[100001];
// clear[x] = true neu toa tau x co the dc don dep
// mac dinh clear[] = false;

void process() {
    // xet tu trai sang phai, tau nao di dc sang trai thi cu cho no di
    for (int i = 0; i < n; i++) {
        if (i == 0) {   // toa tau dau tien tu trai sang phai
            if (isHead[i]) clear[i] = true; // neu no la dau tau => true
        } else {
            if (connect[i-1]) clear[i] = clear[i-1];
            else if (isHead[i]) clear[i] = clear[i-1];
        }

        // break vi bi toa tau nay chan, khong co y nghia gi khi duyet them nua
        if (clear[i] == false) break;
    }

    // xet tu phai sang trai, tau nao di dc sang phai cu cho no di
    for (int i = n-1; i >= 0; i--) {
        if (clear[i]) break;
        // toa tau nay da dc clear, vong lap tren da chay den day
        // NOTE: Thuat toan co the dung tai day va in ra "YES"
        
        if (i == n-1) { // toa tau dau tien tu phai sang trai
            if (isHead[i]) clear[i] = true;
        } else {
            if (connect[i]) clear[i] = clear[i+1];  // neu toa i noi voi toa i+1, no se clear neu toa i+1 clear
            else if (isHead[i]) clear[i] = clear[i+1]; // neu toa i la toa Head, no se clear neu toa i+1 clear
        }

        // break vi bi toa nay chan
        if (clear[i] == false) break;
    }
}

void output() {
    // YES xay ra neu tat ca toa tau deu clear
    for (int i = 0; i < n; i++)
        if (clear[i] == false) {
            cout << "NO\n";
            return;
        }
    cout << "YES\n";
}

int main() {
    input();
    process();
    output();
}
```