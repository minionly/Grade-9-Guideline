# THUẬT TOÁN VÉT CẠN
### Đã bao giờ bạn có ý định mò mẫm mật khẩu, mã pin thiết bị di động của ai đó và thử từng số một chưa? Hay bạn đã từng cố gắng lục tung mọi ngóc ngách trong nhà để tìm kiếm thứ gì đó? Thế thì bạn đã biết “vét cạn” rồi đấy!
## **I. Mục tiêu bài học**
1 Nắm được khái niệm về “vét cạn” - 10%</p>
2 Vận dụng được “vét cạn” trong mọi bài toán - 55%</p>
3 Biết cải thiện thuật toán để tối ưu hóa code - 35%</p>
## **II. Lý thuyết**
1. Khái niệm:
Thuật toán vét cạn hay duyệt trâu (Brute Force) được hiểu đúng như tên gọi của
nó, chúng ta sẽ dùng những phương pháp đơn giản nhất để duyệt qua toàn bộ các
trường hợp của bài toán. Khí đó, ta chắn chắn tìm được đáp án chính xác.
Ví dụ: Bạn muốn truy cập vào một chiếc laptop hay điện thoại mà không biết
mật khẩu, bạn có thể thử qua từng dãy số một đến khi nhập đúng. Như “1”; ”2” ; ...;
“123”; “124”; ...; N-1; N (N là mật khẩu chính xác)
2. Phân tích:
Qua ví dụ trên, có thể thấy rằng: trong mọi vấn đề, bạn luôn tìm được ít nhất
một lời giải hợp lý. Tuy nhiên, chính vì phải duyệt qua tất cả các đáp án nên thuật
toán này mất rất nhiều thời gian để thực hiện. Như kiểu nếu mật khẩu của chiếc
điện thoại quá dài thì sẽ mất rất nhiều thì giờ để tìm ra được dãy số chính xác (giả
sử không bị vô hiệu hóa nếu nhập sai).
Tương tự khi viết chương trình, nếu bạn sử dụng giải thuật vét cạn thì luôn đảm
bảo tìm được kết quả đúng. Nhưng nếu dữ liệu đầu vào quá lớn sẽ dẫn đến lỗi TLE
(Time Limit Exceeded - chạy quá thời gian cho phép)
II. Lý thuyết
3. Bài toán cụ thể:
Cho dãy số A có N phần tử (A[i] < 101) nhập từ bàn phím. Tìm dãy con B có M
phần tử từ dãy A (M <= N < 1001) sao cho tổng các phẩn tử của dãy B lớn nhất có
thể. (Dãy con là những phần tử liên tiếp nhau trong mảng).
- Dữ liệu vào: dòng đầu tiên lần lượt là 2 số N, M. Dòng thứ hai là N số nguyên A[i].
- Kết quả: dãy B có tổng lớn nhất tìm được.
- Ví dụ:</p>
    
    | INPUT         | OUTPUT        |
    | ------------- | ------------- |
    | 6 4</p> 1 -3 2 -5 4 3 | 2 -5 4 3      |
- Solution:
  + Trước tiên hãy phân tích đề bài và xét cần bao nhiêu vòng lặp để thực hiện,
  nhiệm vụ của mỗi vòng lặp là gì?
  Ở bài toàn này, theo phương pháp vét cạn cơ bản, chắc chắn bạn sẽ cần 2 vòng
  lặp lồng nhau. Cụ thể như sau:
  + Trước tiên, cho biến lưu kết quả (ketqua) chứa tổng của M phần tử đầu tiên
  trong mảng A. Vì M phần tử đầu tiên trong mảng A chính là dãy con B khả thi
  đầu tiên.
  + Vòng lặp bên ngoài để tìm tất cả dãy con B khả thi: Ta thấy M phần tử cuối
  của mảng A chính là dãy con B cuối cùng có thể là đáp án. Do đó, chỉ duyệt đến
  N-M+1.
  + Vòng lặp bên trong để tính tổng các phần tử của dãy B đang xét (sum). Sau
  mỗi lần lặp, phải so sánh tổng vừa tìm được với tổng đang lưu (ketqua).
  + Nếu tổng vừa tính lớn hơn hoặc bằng kết quả đang lưu, ta cập nhất kết quả
  mới và lưu vị trí của dãy B mới vào position (vị trí của một dãy con thường được
  hiểu là vị trí phần tử đầu tiên trong dãy).
  + Cuối cùng, ta xuất ra M phần tử từ vị trí đã lưu. Đây là đáp án cần tìm.
  ⟶ Với 2 vòng lặp lồng nhau thì độ phức tạp của bài toán là O(N*M).
- Code mẫu C++:
  ```c++
     #include <bits/stdc++.h>
    using namespace std;
    int a[1005], n, m;
    int ketqua = 0, position = 0;
    
    int main() 
    {
        cin>>n>>m;
        for (int i=1; i<=n; i++) 
        {
            cin>>a[i];
            if (i<=m) ketqua += a[i];
        }
        for (int i=1; i<=n-m+1; i++)
        {
            int sum=0;
            for (int j=1; j<=m; j++) sum += a[j+i-1];
            if (sum >= ketqua)
            {
                ketqua = sum;
                position = i;
            }
        }
        for (int i=position; i<=position+m-1; i++) cout<<a[i]<<" ";
        return 0;
    }

