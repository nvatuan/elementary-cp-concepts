# (Ứng dụng thư viện) Sắp xếp

Thuật toán Sắp xếp là một trong những thuật toán quan trọng nhất của IT, bởi vì nhờ chúng mà chúng ta mới có thể trật tự hóa dữ liệu vào, rồi từ đó, các thuật toán xử lý khác sẽ chạy hiệu quả hơn. Thuật toán Sắp xếp này rất quan trọng nên mọi ngôn ngữ lập trình thời nay đều đã có sẵn một hàm riêng dùng để sắp xếp.

Tất cả các Thuật toán sắp xếp hiện đại được sử dụng thời nay đều chạy với Độ phức tạp là `O(N * log N)`.

Thông thường, thuật toán sắp xếp sẽ đi kèm với một thuật toán khác thì mới giải quyết được bài toán, nên phần này chúng ta sẽ không có bài tập ứng dụng.

## C++

Hàm sắp xếp của `C++` nằm trong namespace `std` và trong file header `<algorithm>`. Tên đầy đủ của nó là `std::sort`. Mặc định, nó sẽ sắp xếp các số theo thứ tự tăng dần về giá trị, hay tăng dần về sự xuất hiện trong từ điển nếu so sánh chuỗi ký tự.

```cpp
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;

int main() {
    // Sort array
    int a[] = {3, 1, 5, 4, 2};
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    std::sort(a, a+5);
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';

    // Sort vector
    vector<int> v = {3, 1, 5, 4, 2};
    for (int i = 0; i < 5; i++) cout << v[i] << ' '; cout << '\n';
    std::sort(v.begin(), v.begin() + 5);
    // hoặc std::sort(v.begin(), v.end()) vì v chỉ có kích cỡ = 5
    for (int i = 0; i < 5; i++) cout << v[i] << ' '; cout << '\n';
}
```


### Ngữ pháp

#### Sort mặc định (thông số thứ nhất và thông số thứ hai)
`std::sort()` của C++ sẽ nhận 2 thông số, thông số đầu tiên là **con trỏ** đến phần tử đầu tên trong đoạn bạn muốn sort, thống số thứ hai là **con trỏ vào phần tử phía sau** của phần tử cuối trong đoạn bạn muốn sort. Hình dung như sau:

```
a[]  =  { 3, 2, 5, 1, 4, 7, 6 }
          ^     ^    muốn sort 3 phần tử này
         +0 +1 +2 +3
=> std::sort(a, a + 3); // a + 3 trỏ đến phần tử cuối của vùng cần sort
=> a[] = { 2, 3, 5, 1, 4, 7, 6 }
```

Đa số các hàm Thuật toán trong `C++` nói riêng và các ngôn ngữ khác nói chung mà xử lý trên một đoạn phần tử đều ứng dụng cách viết "nửa đoạn" này. "Nửa đoạn" (half-range) được mô tả bằng ký hiệu `[L, R)`, mà `L` trỏ đến phần tử đầu tiên trong đoạn mà muốn xử lý, `R` trỏ quá phần tử cuối của đoạn đó 1 phần tử.

#### Sort theo thứ tự nhất định (thông số thứ ba)
`std::sort()` của `C++` còn có một biến thể, giúp nhận một thông số thứ 3 là một đối tượng "function", ở đây, chúng ta sẽ chỉ nghiên cứu về việc sử dụng function để sort:

Ví dụ cho sort theo thứ tự giảm dần

```cpp
#include<iostream>
#include<algorithm>
using namespace std;

bool compare(int a, int b) {
    return a > b;
}

int main() {
    // Sort array
    int a[] = {3, 1, 5, 4, 2};
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    // In ra: 3 1 5 4 2

    std::sort(a, a+5);
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    // In ra: 1 2 3 4 5

    std::sort(a, a+5, compare);
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    // In ra: 5 4 3 2 1
}
```


Trên là một ví dụ cho việc sort bằng hàm cụ thể của người dùng. Hàm `compare()` được sử dụng sẽ nhận 2 giá trị, trả về `true` nếu giá trị đầu tiên lớn hơn giá trị thứ hai. Bạn hãy để ý rằng phần tử đầu tiên trong mảng sau khi được sort, sẽ luôn trả kết quả `true` với các phần tử khác trong mảng nếu được gọi bằng hàm `compare()`. Điều này là vì tính chất bắc cầu của điều kiện.

Ví dụ cho sort theo giá trị tuyệt đối:

```cpp
#include<iostream>
#include<algorithm>
using namespace std;

bool compare(int a, int b) {
    return abs(a) < abs(b);
}

int main() {
    // Sort array
    int a[] = {-3, 1, -5, -4, 2};
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    // In ra: -3 1 -5 -4 2

    std::sort(a, a+5);
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    // In ra: -5 -4 -3 1 2

    std::sort(a, a+5, compare);
    for (int i = 0; i < 5; i++) cout << a[i] << ' '; cout << '\n';
    // In ra: 1 2 -3 -4 -5
}
```

Ở ví dụ trên, hàm sort ở giữa sẽ vẫn giữ thứ tự giá trị tăng dần, trong khi hàm sort cuối cùng sẽ trả về thứ tự tăng dần theo giá trị tuyệt đối.

## Java
Trong `Java` nói thẳng ra là phức tạp hơn C++. Để sort một mảng thuần, bạn sử dụng `Arrays.sort()`. Nhưng đối với các mảng động như `ArrayList`, .. hay là các cấu trúc dữ liệu mà bạn sử dụng trong thư viện `Collections` của `Java`, bạn phải sử dụng `Collection.sort()` thì mới có thể trực tiếp sort chúng, không thì bạn phải convert chúng sang mảng thuần.

### Sort mảng thuần theo thứ tự mặc định
Ví dụ:

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] a = new int[] { 3, 1, 5, 2, 4 };
        for (int i = 0; i < 5; i++) System.out.print(a[i] + " "); System.out.println("");

        Arrays.sort(a);
        for (int i = 0; i < 5; i++) System.out.print(a[i] + " "); System.out.println("");
    }
}
```

### Sort nửa đoạn [L, R) trong mảng thuần theo thứ tự mặc định
Hàm `Arrays.sort()` của `Java` có một biến thể là nhận thêm hai thông số là hai index `L` và `R` đại diện cho half-range `[L; R)` mà bạn muốn sort.

Ví dụ:

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] a = new int[] { 3, 1, 2, 5, 4 };
        for (int i = 0; i < 5; i++) System.out.print(a[i] + " "); System.out.println("");
        // In ra: 3 1 2 5 4 

        Arrays.sort(a, 0, 3); // [0, 3), phần tử 3 là phần tử quá phần tử cuối một phần tử
        for (int i = 0; i < 5; i++) System.out.print(a[i] + " ");  System.out.println("");
        // In ra: 1 2 3 5 4
    }
}
```

### Sort một cấu trúc dữ liệu trong Collections
Trong `Java` còn có `Collections.sort()` hỗ trợ sort các cấu trúc dữ liệu trong thư viện `Collection`. Cụ thể, hàm này sẽ nhận một đối tượng có `implement interface List` ví dụ như: `ArrayList`, `LinkedList`, `Vector`, ... và sort chúng.

Ví dụ với ArrayList:

```java
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> v = new ArrayList<> ();
        v.add(3); v.add(1); v.add(2); v.add(5); v.add(4);

        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: 3 1 2 5 4

        Collections.sort(v);
        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: 1 2 3 4 5
    }
}
```


Về các cấu trúc dữ liệu khác, các bạn có thể search thêm, nếu bao gồm cả chúng thì tài liệu này sẽ rất dài ;v.

### Sort một cấu trúc dữ liệu trong Collections theo một trật tự cụ thể (sử dụng Comparator)

Hàm `Collection.sort()` của `Java` có một biến thể giúp nó nhận thêm một thống số thứ hai là một đối tượng có `implement interface Comparator`. Thông qua đối tượng này, `Java` sẽ so sánh hai đối tượng đó và sắp xếp thứ tự của chúng.

Ví dụ dưới đây tạo một `class Compare` và `implements Comparator`, vì chúng ta biến danh sách của chúng ta sẽ chứa đối tượng `Integer` nên việc tốt nhất là viết chúng ra thẳng luôn. Sau đó, điều còn lại duy nhất là `override hàm compare()`.

Hàm `compare` sẽ nhận hai đối tượng có kiểu tương đồng với kiểu mà chúng ta khai báo với `Comparator<>`. Hàm này trả về `1, 0` hoặc `-1` ứng với `a > b, a == b, a < b`.

Ví dụ với ArrayList, sắp xếp theo thứ tự giảm dần:

```java
import java.util.ArrayList;
import java.util.Collections;

import java.util.Comparator;

class Compare implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        if (o1 > o2) return -1;
        if (o1 == o2) return 0;
        return 1;
    }
}

public class a {
    public static void main(String[] args) {
        ArrayList<Integer> v = new ArrayList<> ();
        v.add(3); v.add(1); v.add(2); v.add(5); v.add(4);

        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: 3 1 2 5 4

        Collections.sort(v, new Compare());
        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: 1 2 3 4 5
    }
}
```


Tóm tắt lại, các việc bạn cần làm để Sort một cấu trúc dữ liệu trong Collections theo một trật tự cụ thể (sử dụng Comparator) là:
1. Tạo một `class` mà `implements interface Comparator`. Nếu có thể hãy viết luôn kiểu dữ liệu mà `Comparator<>` sẽ so sánh, nếu để trống thì kiểu đó được mặc định là kiểu `Object` rồi để sử dụng bạn sẽ phải ép kiểu trong hàm `compare()`.
2. Viết đè định nghĩa hàm `compare(a, b)`. Hàm này trả về kiểu `int`, `-1` hoặc `1` nếu `a` khác `b` theo thứ tự bạn muốn. Còn lại thì trả về `0`.
3. Gọi `Collections.sort()`, thông số một là cấu trúc dữ liệu kiểu `implements List`, thông số thứ hai là **một đối tượng implements interface Comparator** mà bạn đã viết.

Ví dụ với ArrayList, sắp xếp theo giá trị tuyệt đối:
```java
import java.util.ArrayList;
import java.util.Collections;

import java.util.Comparator;

class Compare implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        if (Math.abs(o1) < Math.abs(o2)) return -1;
        if (Math.abs(o1) > Math.abs(o2)) return 1;
        return 0;
    }
}

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> v = new ArrayList<> ();
        v.add(-3); v.add(-1); v.add(2); v.add(5); v.add(-4);

        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: -3 -1 2 5 -4

        Collections.sort(v);
        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: -4 -3 -1 2 5

        Collections.sort(v, new Compare());
        for (int i = 0; i < 5; i++) System.out.print(v.get(i) + " "); System.out.println("");
        // In ra: -1 2 -3 -4 5
    }
}
```

Một lưu ý cuối cùng là `comparator` của bạn phải đảm bảo tính chất bắc cầu, nếu không `Java` sẽ báo lỗi.

## Kết lời
Thông thường chúng ta chỉ sẽ sắp xếp theo thứ tự mặc định, nhưng sẽ có nhiều trường hợp chúng ta cần phải sắp xếp theo một thứ tự hoàn toàn khác mới có thể giải quyết được bài toán.

Bài viết còn chưa nhắc đến việc sắp xếp các Đối tượng do người dùng viết, vì trong thực tế, chúng ta sử dụng lập trình hướng đối tượng để mô phỏng đời sống, dữ liệu thực sự không chỉ là một số nguyên hay một số thực, nó là một tập hợp các số.

## Tham khảo thêm

### Java: Chỉ tập trung vào thư viện Collections:

[Sắp xếp Collection trong Java, @Topdev.vn](https://topdev.vn/blog/java-collections-huong-dan-sap-xep-trong-collections-cua-java/)

[Sắp xếp Collection trong Java, @Viblo.asia](https://viblo.asia/p/sap-xep-collection-trong-java-V3m5WEvxZO7)

### Java: Tài liệu toàn vẹn hơn:

[Sắp xếp trong Java8](https://gpcoder.com/4009-sap-xep-trong-java-8/)  _dịch của_  [Sorting in Java](https://www.baeldung.com/java-sorting)