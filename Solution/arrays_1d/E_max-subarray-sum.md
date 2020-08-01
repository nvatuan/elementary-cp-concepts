# Arrays 1D - E - Tổng mảng con lớn nhất

[Về Index](index.md)

## Lời giải O(N*N)

Độ phức tạp cho phép Thuật toán `O(N*N)`, tương ứng với việc cho phép chúng ta duyệt qua mọi mảng con của mảng chính. Từ đó ta có thể lấy tổng lớn nhất trong số đó.


## Lời giải O(N)

Thuật toán Kadane là một thuật toán nổi tiếng, search đi :v



## Code nguồn O(N*N)

```cpp
#include <iostream>
using namespace std;

int n;
long long a[100001];

void input() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];
}

long long bestSum;
long long currentSum;

void process() {
    bestSum = a[0];
    
    for (int i = 0; i < n; i++) {
        currentSum = 0;
        for (int j = i; j < n; j++) {
            currentSum += a[j];
            bestSum = max(bestSum, currentSum);
        }
    }
}

void output() {
    cout << bestSum << '\n';
}

int main() {
    input();
    process();
    output();
}
```

## Code nguồn O(N)

```cpp
#include <iostream>
using namespace std;

int n;
long long a[100001];

void input() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];
}

long long bestSum;
long long currentSum;
void process() {
    bestSum = a[0];
    currentSum = 0;

    for (int i = 0; i < n; i++) {
       currentSum = max(a[i], currentSum + a[i]);
       bestSum = max(bestSum, currentSum);
    }
}

void output() {
    cout << bestSum << "\n";
}

int main() {
    input();
    process();
    output();
}
```