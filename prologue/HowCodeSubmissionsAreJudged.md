[<< Về trang chính](../index.md)

# Cách thức mà bài Code được chấm điểm

Một chương trình/code hợp lệ chỉ khi nó: biên dịch thành công, chạy và thoát thành công, chạy trong thời gian quy định và cho ra được kết quả đúng với mọi tập dữ liệu vào. Điều này luôn đúng với mọi code project, kể cả việc bạn đang làm việc cho người khác hay làm việc một mình. 

Khi đi làm, code của bạn sẽ được review tính đúng đắn và tính thực thi thông qua một hệ thống tự động. Còn tính ngay ngắn sẽ được review bởi người. Lý do cho việc này là tính ngay ngắn hay thẩm mỹ là một phạm trù chủ quan (tuy có phần khách quan) như code phải cách đầu dòng 2 dấu cách hay 1 dấu Tab, còn tính đúng đắn và tính thực thi là hoàn toàn khách quan, máy móc sẽ đảm bảo việc này.

Các tiêu chí trên cũng tồn tại trong Lập trình thi đấu. Dựa vào điều này, các yếu tố quan trọng đã được rút ra về một bài Code khi đang được xem xét trên hệ thống:

## I. Ngữ pháp hợp lệ
Ngữ pháp hợp lệ khi chương trình đó được biên dịch thành công. Nếu chương trình bạn không biên dịch thành công trên hệ thống chấm, hệ thống sẽ thông báo Compilation Error (hoặc là CE). Một vài hệ thống sẽ báo lỗi tại đâu trong code của bạn (tuy nhiên bkdnOJ không có).

Nếu như code bạn biên dịch được trong máy của mình nhưng gặp lỗi trên hệ thống, có thể do các nguyên nhân sau, được sắp xếp theo mức độ thường xuyên xảy ra:
1. Nguyên văn code bị sai lệch.
    - Điều này xảy ra khi một vài kí tự không hợp lệ có trong code của bạn. Có thể IDE của bạn đã chỉnh sửa code nguyên văn nhưng không hợp lệ của bạn thành code hợp lệ để rồi biên dịch. Bạn có thể kiểm tra điều này bằng cách biên dịch thủ công `g++ code.cpp` hoặc `javac code.java` và xem output lỗi.
    - Để tránh điều này xảy ra, code của bạn không nên có ký tự khác bảng ký tự ASCII, tức là các ký tự mà được in trên bàn phím của bạn. Ví dụ như ký tự `ư` không hề có.

2. Khác phiên bản bộ biên dịch. 
    - Thông thường điều này rất ít khi xảy ra, vì phần mềm thời nay được phát triển theo tư tưởng tương thích lùi (backward compatibility), tức là phiên bản hiện đại hơn phải hiểu được phiên bản cũ hơn, một ví dụ cho việc này là một người N3 ít nhất phải làm được đề N4 :v. Tuy nhiên, khả năng này vẫn có thể xảy ra)

3. Khác ngôn ngữ biên dịch.
    - ¯\\\_(ツ)\_/¯

## II. Lỗi thời gian chạy
Lỗi thời gian chạy (Runtime Error, RE, RTE,...) là một lỗi xảy ra khi chương trình của bạn đang chạy. Lỗi này được sinh ra từ việc chương trình bạn thực hiện một hành động không hợp lệ (ví dụ như hành động chia một số cho 0, là một hành động không được định nghĩa trong toán học). Một vài ngôn ngữ hiện đại như Python, Ruby,.. không cần biên dịch trước khi chạy, vì vậy có một số lỗi thời gian chạy thực chất là do lỗi ngữ pháp.

Các lý do thường xuyên xảy ra:
1. Chia cho 0:
    - Xảy ra khi một số nguyên chia cho một số nguyên 0.
2. Tràn mảng:
    - Khi Mảng được cấp có vùng xác định là từ \[0\] tới \[N-1\] mà bạn truy cập vào phần tử quá N-1 hoặc là số âm.
3. Đệ quy quá nhiều lần:
    - Chương trình đệ quy có sử dụng một Stack để lưu thông tin. Mỗi lần bạn gọi một hàm đệ quy, nó giống như khi bạn đang ở tầng 1 đi lên tầng 2 vậy. Bạn cứ gọi đệ quy mãi tương ứng với việc bạn cứ đi lên mãi, sẽ có lúc bạn lên tới tầng thượng, khi đó bạn không thể lên được nữa. Gọi đệ quy tại lúc mà bạn đã đụng giới hạn sẽ sinh ra RE.
    - Thuật ngữ cho việc này là (Recursion) Stack Overflow.
    - Thông thường, giới hạn của Stack này là rất lớn. Stack của bkdnOJ lên đến 2*10^7 tầng (đã test).
4. Một số lỗi khó nhận biết khác:
    - Cấp phát động một khoảng là `int abc` nhưng `abc` ở đây có giá trị âm.
    - Ngôn ngữ Java là ngôn ngữ nghiêm khác hơn nhiều so với C++. Khi bạn tạo một đối tượng chưa được khởi tạo, nó mặc định sẽ bằng `null`. Tương tác với `null` sẽ xảy ra lỗi `NullPointerException`.

## III. Giới hạn thời gian chạy
Là thời gian cho phép chương trình của bạn chạy. Nếu chương trình của bạn chạy hơn giới hạn một chút, nó sẽ bị ngừng bởi trình chấm, mặc kệ output của code. Khi đó, bạn sẽ nhận được thông báo Time Limit Exceeded (hay TLE).

### Tóm tắt Độ phức tạp Thuật toán
Giả sử bạn được cấp một tập hợp các số nguyên `S` ngẫu nhiên và được yêu cầu tính tổng của tất cả số đó. Cách duy nhất để luôn có đáp án đúng là bạn phải đi qua mỗi số trong tập hợp đó, lần lượt cộng từng số một. Giống như việc bạn tự hỏi trong ví mình có tổng cộng bao nhiêu tiền vậy, bạn phải đi qua từng tờ tiền để có được tổng tiền chính xác. Nếu số tờ tiền nhiều lên (tiền lẻ), bạn phải cộng nhiều hơn. Điều này thể hiện mối quan hệ của Hành động tính tổng và Số lượng phần tử, nói chung hơn là Độ phức tạp thời gian và Độ lớn của Tập dữ liệu.

### Xác định Độ phức tạp Cho phép
Tất cả những hệ thống chấm bài đều yêu cầu chương trình bạn tạo ra kết quả trong một khoảng thời gian nhất định, mà tiêu biểu là trong `1 second`. Thời gian quy định, code của bạn phải tạo ra được kết quả chính xác với một tập dữ liệu có kích cỡ tối đa là `N`. Tại đây, bạn đã có thời gian tối đa được chạy và giới hạn tối đa của tập dữ liệu, có cách nào để từ hai thông số này mà tìm được thuật toán cho phép không? Câu trả lời là có.

Tuy không hoàn toàn chính xác, nhưng đây là các tiêu chí sẽ là kim chỉ nam giúp định hướng cho bạn về độ phức tạp thời gian mà bạn nên có.

| Độ lớn Tối đa của Dữ liệu | Các thuật toán kết thúc trong 1s |
|---------------------------|----------------------------------|
| N = 100 000 000           | O(N)                             |
| N = 1 000 000             | Trên hoặc O(N log N)             |
| N = 10 000                | Tất cả trên hoặc O(N^2)          |
| N = 100                   | Tất cả trên hoặc O(N^3)          |
| N = 50                    | Tất cả trên hoặc O(N^4)          |
| N = 20                    | Tất cả trên hoặc O(2^N)          |
| N = 11                    | Tất cả trên hoặc O(N!)           |

Một quan sát nữa là Để chấm bài các bạn, người ra đề phải giải được bài toán đó. Vậy, bài toán bạn đang giải là một bài toán có lời giải. Vì vậy bạn có thể chắc chắn rằng nó là bài toán có thể giải được trong độ phức tạp nhất định, trong thời gian nhất định. Nếu bạn nghĩ rằng người ra đề code thuật toán chậm và để nó chạy 1 năm rồi lấy dữ liệu đó yêu cầu bạn giải quyết nó trong 1 giây thì bạn nên đi viết Thuyết âm mưu.

Hơn nữa, có thể Thuật toán bạn sử dụng để giải không phải là thuật toán tối ưu nhất, hoặc có thể nó là thuật toán tối ưu nhất, điều đó sẽ không quan trọng miễn là nó luôn tạo ra được Kết quả chính xác **VÀ** kết thúc kịp thời.

Một cách khác để ước lượng tốc độ chương trình của bạn là: 
Bạn sẽ tính N = **tích các phần lồng nhau trong code của bạn**, bỏ các dấu `+`, `-` đi.

Giả sử, xét đoạn code sau:
```cpp
int result = 0;
for (int i = 0; i < n; i++)             // chạy N lần
    for (int j = 0; j < m; j++) {       // - mỗi N lần, chạy M lần           
        int u = 1;
        while (u < k) {                 // -- mỗi M lần, nhân 2 bản thân lên cho đến K => chạy log2 của K lần
            result += u;
            u *= 2;
        }
        for (int r = 2; r < 5; r++)    // -- mỗi M lần, chạy 3 lần
            if (result % r == 0) cout << "Chia het cho " << r << '\n';
    }
```

Bên trên là một đoạn code gồm nhiều phần xử lý, cách tính là bạn sẽ nhân những lần lặp lồng nhau đó lại: `N = n * m * (log(k) + 3)`.
Ở đây, bạn sẽ vứt đoạn + 3 đi. Lý do cho việc này là khi dữ liệu lớn lên rất nhiều, việc + hay - một hằng số không có ý nghĩa gì nữa, để đơn giản hơn thì ta nên vứt phần đó đi.
Vậy, `N = n*m*log(k)`, nếu n, m, k có giới hạn là 100 thì N = `100*100*log100 ~= 8*10^4`.

Nếu `N` nhỏ hơn 100 triệu (10^8) thì code của bạn sẽ kết thúc trước `1s`.

Trên thực tế, việc xác định này khó hơn nhiều, vì không phải lúc nào một biến lặp luôn được tăng lên một khoảng cố định, hay là điều kiện lặp luôn là một phép so sánh.

## IV. Kết quả output
Nếu code của bạn cho ra kết quả sai, trình chấm sẽ thông báo Wrong Answer (hay WA). Lý do cho ra Wrong Answer:
1. Thuật toán Sai thật.
2. Thuật toán Đúng nhưng do lý do lỗi tràn số, giả dụ như biến `int` chỉ chứa được đến 10^9 phải chứa một số là 10^10.
3. Do hành vi không được định nghĩa (Undefined Behaviour). Có thể trình IDE của bạn tự động khởi tạo giá trị mặc định cho một biến là `0`, nhưng điều này có thể sẽ khác với các hệ thống khác. Tiêu biểu là hành động tạo một biến `int` trong hàm `main` trong `C/C++`. Giá trị này là một số ngẫu nhiên, nhưng có thể nó mang giá trị `0` trong hệ thống của bạn.
4. Một vài lý do rất hãm là dòng cuối cùng của bạn không có ký tự `\n`. Điều này còn tùy hệ thống, khi xảy ra thì nó sẽ luôn xảy ra, nghĩa là nếu bạn sai ngay Test đầu tiên thì khả năng cao là bạn nên thử in thêm ký tự `\n`.

Hiện nay, các hệ thống chấm đang dần chuyển qua sử dụng `Checker`, nó là một chương trình kiểm tra tính đúng của chương trình bạn, động lực cho việc này là do một bài toán có nhiều lời giải và người ra đề không muốn giới hạn bạn trong một khuôn khổ, điều này sẽ giới hạn sự sáng tạo trong cách viết lời giải.

## V. Bộ nhớ sử dụng
Bộ nhớ sử dụng là một trong những thông số không quan trọng, tuy nhiên, nếu chương trình của bạn sử dụng một Cấu trúc dữ liệu ứng dụng cấp phát động (ví dụ như cây nhị phân, ...) bạn có thể vô tình sử dụng quá nhiều bộ nhớ và bị lỗi Memory Limit Exceeded (MLE). Tuy nhiên, điều này rất hiếm khi xảy ra, vì máy tính hiện đại có rất nhiều bộ nhớ.

Bộ nhớ thông thường được cho phép thường xấp xỉ `10^8` số `int 32-bit`.

# Các tài liệu đọc thêm, kinh nghiệm của các người đi trước:
[@VNOI: Tìm ra Lời giải](https://vnoi.info/wiki/translate/topcoder/How-to-Find-a-Solution.md)

[@VNOI: Cách tiếp cận một vấn đề 1](https://vnoi.info/wiki/translate/topcoder/Planning-an-Approach-to-a-Topcoder-Problem-Part-1.md)

[@VNOI: Cách tiếp cận một vấn đề 2](https://vnoi.info/wiki/translate/topcoder/Planning-an-Approach-to-a-Topcoder-Problem-Part-2)

[@VNOI: Độ phức tạp Tính toán 1](https://vnoi.info/wiki/translate/topcoder/Computational-Complexity-Section-1.md)

[@VNOI: Độ phức tạp Tính toán 2](https://vnoi.info/wiki/translate/topcoder/Computational-Complexity-Section-2)