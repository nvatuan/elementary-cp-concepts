[<< Về trang chính](../index.md)

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

[Link Contest Practice Arrays 1D](https://codeforces.com/contests/289360)

- [Link Lời giải Arrays 1D](../Solution/arrays_1d/index.md)

[Link Contest Practice Arrays 2D](https://codeforces.com/contests/289569) 

- [Link Lời giải Arrays 2D](../Solution/arrays_2d/index.md)

### 1. Xử lý thông tin chứa trong mảng
Đây là công dụng chủ yếu của mảng, bạn lưu trữ nó, rồi xử lý thông tin đó. Phần lớn các yêu cầu trong mục này có thứ tự truy cập các phần tử mảng luôn cố định (từ trái qua phải, hoặc từ phải qua trái, ...).

* Mảng 1D:

    - A - In ngược mảng
    - B - Tìm "password"
    - D - Cắt cỏ kiểu Máy đánh bạc
    - E - Subarray có tổng lớn nhất
    - F - Truy vấn Tổng 1D Easy

* Mảng 2D Áp dụng:

    - A - Tic Tac Toe
    - B - Chữ thập thăng
    - C - Room Rental
    - D - Rào hố đất
    - E - Truy vấn Tổng 2D Easy


### 2. Sử dụng chỉ số i như là đại diện cho một đối tượng 
Xét một phần tử mảng, ví dụ như `A[i]`, `A[i]` thật ra chứa đến 2 nguồn thông tin, đó là chỉ số `i` và phần tử `A[i]`. Việc nhận ra điều này sẽ cho phép bạn có ý tưởng sáng tạo hơn. 

* Mảng 1D Áp dụng:

    - C - Vắng mặt
    - G - Dọn dẹp đường ray
    - H - Dưới quyền điều hành

* Mảng 2D Áp dụng:

    - F - Forking Knight move
    - G - Sàn nhảy
    - H - Khôi phục thứ tự

Việc sử dụng chỉ số `i` như đại diện cho một đối tượng này dẫn đến sự xuất hiện của cấu trúc dữ liệu Hash Tables và ý tưởng biểu diễn một đối tượng bất kỳ bằng một dãy số nguyên, nếu bạn muốn tìm hiểu thêm.

## Kết lời
Trong tin học, phần tử bắt đầu hay được gọi là phần tử thứ 0, danh sách các phần tử được đánh số từ 0. Điều này hay mâu thuẫn với toán học, nơi muốn bắt đầu đánh số thứ tự của một chuỗi số hay một mảng số từ 1 (Matlab).
