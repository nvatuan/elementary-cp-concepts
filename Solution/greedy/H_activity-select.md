# Greedy - H - Sắp xếp công việc

[Về Index](index.md)

## Hint giải & Lời giải
Bài này đã được nhắc đến ở [trang chính của Giải thuật tham lam](../../BasicAlgorithm/Greedy.md#4-sắp-xếp-công-việc). Mục đích của bài chỉ để test code.

## Code giải
```cpp
#include <iostream>
#include <algorithm>
#include <climits>
using namespace std;

int n;

class Job {
    public:
        long long start, finish;
        Job() {}
        Job(long long s, long long f) { start = s; finish = f; }
};
Job jobs[100001];

void input() {
    cin >> n;
    for (int i = 0; i < n; i++)
        cin >> jobs[i].start >> jobs[i].finish;
}

// -- comparator
bool finishFirst(Job a, Job b) {
    if (a.finish < b.finish) return true;
    return false;
}

int ans = 0;
void process() {
    sort(jobs, jobs + n, finishFirst);

    int lastFinish = -1;
    ans = 0;
    for (int i = 0; i < n; i++) {
        if (lastFinish <= jobs[i].start) {
            ans++;
            lastFinish = jobs[i].finish;
        }
    }

}

void output() {
    cout << ans << endl;
}

int main() {
    input();
    process();
    output();
}
```