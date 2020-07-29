# Mảng

Mảng là một danh sách các phần tử, được tổ chức liên tiếp nhau trên bộ nhớ. Mảng là một cấu trúc dữ liệu đơn giản nhất và rất hiệu quả. Giả sử bạn cần một đoạn mã để tính giá trị trung bình của một vài con số. Mảng là sự lựa chọn tuyệt vời để giữ các giá trị bởi yêu cầu bài toán không đòi hỏi một thứ tự lưu trữ cụ thể và các phép tính toán cũng không đòi hỏi gì khác ngoài việc duyệt qua toàn bộ các phần tử.

## Khai báo

### Mảng tĩnh
Thông thường, bạn sẽ sử dụng mảng để chứa dữ liệu và xử lý chúng trên mảng này. Vì dữ liệu vào thay đổi mỗi lần chạy, mảng của bạn phải đủ lớn đễ chứa được mọi kiểu dữ liệu vào mà bài toán cho.

> Cho một số nguyên dương N (N <= 1000), cho một danh sách gồm N số nguyên. Hãy tính trung bình cộng của chúng.

Với yêu cầu trên, bạn nhận thấy rằng mảng chỉ cần đủ rộng để chứa `1000` phần tử.

### Mảng động
Đối với khai báo động, bạn không cần quan tâm đến giới hạn max của tập dữ liệu. Đề cho bao nhiêu bạn cấp phát bấy nhiêu, rất tiện lợi. Trong thư viện chuẩn của `C++` có kiểu dữ liệu `vector` có thể chứa một loại dữ liệu bất kỳ. Trong thư viện chuẩn của `Java` có kiểu dữ liệu `ArrayList` và `Vector` cũng có thể chứa một loại dữ liệu bất kỳ.

Một ưu thế mà Mảng động có so với Mảng tĩnh là những bài toán có kích cỡ đầu vào linh hoạt, giả sử như:

> Có N học sinh (0 < N < 10^6) là học sinh của một trường nọ, mỗi học sinh là thành viên của chỉ một lớp. Biết trường đó có đến M lớp học (0 < M < 10^6)...

Chúng ta phải lường trước hai trường hợp như: 1 lớp chứa đến 10^6 học sinh, hay 10^6 lớp mỗi lớp đều có học sinh. Nếu sử dụng Mảng tĩnh, chúng ta phải khai báo một ma trận 2 chiều, chiều thứ nhất là số thứ tự của lớp học, chiều thứ hai là số thứ tự của học sinh trong một lớp, điều này đồng nghĩa với việc sử dụng 10^12 không gian bộ nhớ, quá lớn so với nhiều hệ thống.

Trong khi sử dụng Mảng động, chúng ta có thể khởi tạo 10^6 mảng động, mỗi mảng động tượng trưng cho một lớp, và tăng kích cỡ mỗi lớp lên khi thông tin của một học sinh được đọc vào. Điều này đảm bảo không gian bộ nhớ lớn nhất chúng ta sử dụng là 2*10^6.

## Các cách sử dụng thông thường

### 1. Xử lý thông tin chứa trong mảng
Đây là công dụng chủ yếu của mảng, bạn lưu trữ nó, rồi xử lý thông tin đó. Phần lớn các yêu cầu trong mục này có thứ tự truy cập các phần tử mảng luôn cố định (từ trái qua phải, hoặc từ phải qua trái, ...).

<details>
    <summary> Mảng 1D Áp dụng:  </summary>

- [In ngược mảng]()
- Táo
- Tìm "password"
- Cắt cỏ kiểu Máy đánh bạc
- Subarray có tổng lớn nhất
- Truy vấn Tổng 1D Easy
</details>

<details>
    <summary> Mảng 2D Áp dụng:  </summary>

- Tic Tac Toe
- Chữ thập thăng
- Room Rental
- Rào hố đất
- Truy vấn Tổng 2D Easy
</details>

### 2. Sử dụng chỉ số i như là đại diện cho một đối tượng 
Xét một phần tử mảng, ví dụ như `A[i]`, `A[i]` thật ra chứa đến 2 nguồn thông tin, đó là chỉ số `i` và phần tử `A[i ]`. Việc nhận ra điều này sẽ cho phép bạn có ý tưởng sáng tạo hơn. 

#### Mảng 1 chiều:
-   <details>
    <summary> Bài "Vắng mặt" </summary>
    <details>
    <summary> Hint giải </summary>
    Khai báo một mảng `diemDanh[]` và sử dụng chỉ số `i` như là mã số học sinh.
    </details>
    <details>
    <summary> Lời giải </summary>

    Ban đầu, mảng `diemDanh[]` của chúng ta sẽ chứa toàn giá trị `false`, vì lớp học vừa mở cửa và không có ai trong đó cả. Sau đó, chúng ta sẽ lần lượt cho từng học sinh vào và đánh dấu là học sinh đó có mặt. Sau đó chỉ cần duyệt qua tất cả mã số học sinh, in ra các mã số học sinh mà có `diemDanh[i] == false`.

    Giả sử như lớp chúng ta chỉ có 10 hoạc sinh và có các học sinh như sau đi học 11, 14, 15. Gán `diemDanh[3] = true, diemDanh[4] = true, diemDanh[7] = true;`. Sau đó, chúng ta duyệt lần lượt mã số học sinh từ 1 cho đến 10, nếu `diemDanh[mã_số_học_sinh] == false` tức là học sinh đó không có mặt.
                
    </details>
    <details>
    <summary> Code giải </summary>

    [Source](https://pbs.twimg.com/media/Ec5DcA8X0AY2l6Z?format=jpg&name=large)
    </details>
    </details>

-   <details>
    <summary> Bài "Dưới quyền điều hành" </summary>

    <details>
    <summary> Hint giải </summary>

    Khai báo một mảng `boss[]` mà `boss[i]` là mã của nhân viên là cấp trên trực tiếp điều hành nhân viên có mã số là chỉ số `i`.
    Nếu như một nhân viên không có cấp trên thì giá trị `boss[]` của họ là một giá trị đặc biệt (ví dụ như -1). 
    Nếu gặp giá trị này, chúng ta sẽ `return NO`, vì chúng ta biết là họ không có cấp trên.

    Cấp trên của cấp trên của cấp trên của ... của `x` lúc này sẽ là: `boss[boss[boss[...boss[x]...]]]`.
    </details>

    <details>
    <summary> Lời giải </summary>

    Để thuận tiện cho việc cài đặt thuật toán (hay là việc code), chúng ta khai báo một biến `sep` sẽ bằng `boss[x]`.
    Sau đó, sẽ chỉ có thể có hai trường hợp:
    - `sep` vẫn có cấp trên, tức là `boss[sep] != -1` (-1 là giá trị đặc biệt chúng ta gán từ trước)
    - `sep` không có cấp trên, tức là `boss[sep] == -1`

    Chúng ta sẽ liên tục đi lên chuỗi cấp trên của cấp trên đó, liên tục check nếu `sep` có bằng `y` không, nếu có chúng ta sẽ in ra `YES` và dừng truy vấn lên nữa.
    Nếu không phải, chúng ta chỉ dừng khi `sep` không còn cấp trên, lúc này chúng ta sẽ in ra `NO`.
    </details>

    <details>
    <summary> Code giải </summary>

    [Source](https://pbs.twimg.com/media/Ec5DcA8X0AY2l6Z?format=jpg&name=large)
    </details>

    </details>

-   <details>
    <summary> Bài "Nhiều mắc xích" </summary>

    <details>
    <summary> Hint giải </summary>

    lorem

    </details>
    <details>
    <summary> Lời giải </summary>

    lorem.

    </details>
    <details>
    <summary> Code giải </summary>
    
    lorem.

    </details>

    </details>







#### Mảng 2 chiều:
-   <details>
    <summary> Bài "Sàn nhảy" </summary>

    <details>
    <summary> Hint giải </summary>

    lorem

    </details>
    <details>
    <summary> Lời giải </summary>

    lorem.

    </details>
    <details>
    <summary> Code giải </summary>
    
    lorem.

    </details>

    </details>

-   <details>
    <summary> Bài "Khôi phục thứ tự" </summary>

    <details>
    <summary> Hint giải </summary>

    lorem

    </details>
    <details>
    <summary> Lời giải </summary>

    lorem.

    </details>
    <details>
    <summary> Code giải </summary>
    
    lorem.

    </details>

    </details>

Việc sử dụng chỉ số `i` như đại diện cho một đối tượng này dẫn đến sự xuất hiện của cấu trúc dữ liệu Hash Tables và ý tưởng biểu diễn một đối tượng bất kỳ bằng một dãy số nguyên, nếu bạn muốn tìm hiểu thêm.

## Kết lời
Trong tin học, phần tử bắt đầu hay được gọi là phần tử thứ 0, danh sách các phần tử được đánh số từ 0. Điều này hay mâu thuẫn với toán học, nơi muốn bắt đầu đánh số thứ tự của một chuỗi số hay một mảng số từ 1 (Matlab).
