# Arrays 2D - D - Dải số

[Về Index](index.md)

## Hint giải
Bạn có thể đếm số nét cắt bằng cách sử dụng một vòng `for` để duyệt qua mọi vị trí có thể cắt. Sau đó, bạn có thể sử dụng Prefix Sum để lấy tổng bên trái và lấy tổng bên phải rồi kiểm tra xem chúng có bằng nhau không.

Hãy chú ý là hai dải phải có ít nhất một phần tử.

## Lời giải
Để lấy tổng bên trái, ta lấy prefix sum tại vị trí hiện tại. Để lấy tổng bên phải, ta có thể lấy tổng của cả dãy (phần tử cuối của prefix sum) trừ cho tổng bên trái.

**Một cách làm khác là**, ta có thể sử dụng hai prefix sum, một mảng là tổng từ trái sang phải gọi là prefix sum, một mảng là tổng từ phải sang trái gọi là postfix sum. Tổng trái và tổng phải sẽ là prefix sum và postfix sum tại vị trí hiện tại.

## Code nguồn
```cpp
#include <bits/stdc++.h>
using namespace std;

long long arr[2*100001];
long long pfsum[2*100001];

int main(){
	int n;
	cin >> n;
	for(int i = 1; i <= n; i++){
		cin >> arr[i];
		pfsum[i] = pfsum[i-1] + arr[i];
	}
	int answer = 0;
	for(int i = 1; i <= n-1; i++){
		if(pfsum[i] == (pfsum[n]-pfsum[i])) answer++;
	}
	cout << answer;
}
```