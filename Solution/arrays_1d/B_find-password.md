# Arrays 1D - B - Tìm password

[Về Index](index.md)

## Hint giải

Chuỗi ký tự "`password`" có 8 phần tử và chuỗi cần kiểm tra có `n` phần tử.

Chúng ta chỉ cần kiểm tra mọi đoạn có độ dài là `8` trong chuỗi cần kiểm tra, xem thử đoạn đó có nội dung là "`password`" hay không.


## Code nguồn

```cpp
#include <bits/stdc++.h>
using namespace std;

string st;

int check(int k){
	return (
		(st[k] == 'p') && (st[k+1] == 'a') && (st[k+2] == 's') && (st[k+3] == 's')
		&& (st[k+4] == 'w') && (st[k+5] == 'o') && (st[k+6] == 'r') && (st[k+7] == 'd')
	);
}

int main(){
	cin >> st;
	int l = st.length();
	for(int i = 0; i < l - 7; i++){
		if(check(i)) {cout << "YES"; return 0;}
	}
	cout << "NO";
	return 0;
}
```