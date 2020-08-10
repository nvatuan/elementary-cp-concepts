# Arrays 2D - F - Sau cơn mưa

[Về Index](index.md)

## Hint giải
- Hãy vẽ những mực nước cao nhất mà mái nhà có thể chứa ra và xem các mực nước này phụ thuộc vào điều gì? Bạn hãy thử thay đổi chiều cao của một số cột và xem thử cột nào thay đổi thì mực nước nào sẽ thay đổi?
- Xét các cột từ trái sang phải, cột nào không chứa nước và bắt đầu từ cột nào thì mới chứa nước. Sau đó cũng làm tương tự từ phải sang trái.

## Lời giải
<details>
    <summary> Spoiler </summary>
Vì lượng nước chứa trên mái nhà là nhiều nhất, nên lượng nước chứa trên một cột sẽ phụ thuộc vào hai cột cao nhất nằm ở bên trái và ở bên phải cột đang xét. Vì nước sẽ mãi dâng lên cho đến cho đến khi nó trào ra bởi vì nó dâng quá cột mà đang chặn nó.

Chúng ta sẽ tính lượng nước nằm trên mỗi cột và ta sẽ tính tổng nó.

Lượng nước nằm trên mỗi cột sẽ phụ thuộc vào min của cột lớn nhất nằm bên trái và cột lớn nhất nằm bên phải của cột đang xét.

Chúng ta sẽ định nghĩa hai mảng `L[]` và `R[]`, với `L[i]` là cột cao nhất mà nằm bên trái của `i`, và `R[i]` là cột cao nhất nằm bên phải của `i`. Lượng nước nằm trên `i` sẽ là `min(L[i], R[i]) - độ cao của cột i`.
</details>

## Code nguồn

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a (n + 2);
    for(int i = 1; i <= n; i++) cin >> a[i];
    //
    vector<int> L (n+2, 0), R(n + 2, 0);
    for(int i = 1; i <= n; i++) {
        L[i] = L[i-1];
        if(L[i] < a[i]) L[i] = a[i];
    }
    for(int i = n; 0 < i; --i) {
        R[i] = R[i+1];
        if(a[i] > R[i]) R[i] = a[i];
    }

    long long ans = 0;
    for(int i = 1; i <= n; i++) {
        ans += max(0, min(L[i], R[i]) - a[i]);
    }
    cout << ans;
}
```