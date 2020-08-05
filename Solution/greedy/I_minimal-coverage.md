# Greedy - I - Minimal Coverage

[Về Index](index.md)

## Hint giải
- Bài toán cần phải được sắp xếp trước, nhưng phải sắp xếp theo tiêu chí nào đây?
    1. Độ dài đoạn?
    2. Điểm bắt đầu?
    3. Điểm kết thúc?

- Tiêu chí tham lam ở đây là gì? Nếu một vị trí được bao phủ bởi nhiều đoạn thẳng thì nên ưu tiên đoạn thẳng nào?

## Lời giải
Sắp xếp các đoạn thẳng theo thứ tự tăng dầu của điểm bắt đầu.

Ý tưởng sẽ là nếu một điểm được bao phủ bởi nhiều đoạn thẳng thì ta sẽ chọn đoạn mà bao phủ xa nhất có thể. Để làm điều này, ta duy trì hai số nguyên là `L` và `R` với `L` là điểm cần được bao phủ hiện tại và `R` là điểm xa nhất mà một đoạn thẳng bao phủ được `L`, bao phủ tới được.

Lúc đầu, `L` và `R` sẽ bằng `0`. Ta sẽ duyệt qua từng đoạn thẳng một. Nếu `L` nằm gọn trong đoạn thẳng đó thì ta sẽ tối đa hóa `R` (tiêu chí tham lam). Nếu `L` lớn hơn hoặc bằng điểm đầu tiên của đoạn thẳng đang xét thì:
- Nếu `L` < `R` ta biết chắc tồn tại một đoạn thẳng bao phủ `[L, R]` và ta sẽ dùng đoạn thẳng này để đưa `L` đến `R`, ta gán `L` bằng `R` và sau đó tiếp tục duyệt cho đến khi `L` bằng hoặc vượt quá `m`.
- Nếu `L` == `R`, điều này có nghĩa là không còn đoạn thẳng nào bao phủ từ `L` đến điểm đầu tiên của đoạn thẳng đang xét. Bạn có thể dừng chương trình tại đây.

Mỗi lần ta dời `L` đến `R` là một đoạn thẳng được sử dụng. Chúng ta có thể tăng biến đếm tại đây.

**Lưu ý**: Nếu bạn sử dụng kiểm tra `L` có nằm trong đoạn thẳng `i` thay vì kiểm tra tọa độ lớn hay bé thì bạn phải cẩn thận với những đoạn thẳng chỉ nằm trong vùng giá trị âm.

## Code giải
```cpp
#include <bits/stdc++.h>
using namespace std;

int N, M;
vector<pair<int, int>> segs;

void input() {
    cin >> N >> M;
    for (int a, b; N--;) {
        cin >> a >> b;
        segs.push_back({a, b});
    }
}

void solve() {
    sort(segs.begin(), segs.end());

    int Left = 0, Right = 0;
    int ans = 0;
    
    for (int i = 0; i < segs.size(); i++) {
        if (Left < segs[i].first) {
            Left = Right;
            ans++;
        }
        if (M <= Left) break;

        if (segs[i].first <= Left) {
            Right = max(Right, segs[i].second);
        }
    }

    if (Left < M && Left < Right) {
        Left = Right; ans++;
    }

    if (Left < M) printf("-1\n");
    else printf("%d\n", ans);
}

int main() {
    input();
    solve();
}
```