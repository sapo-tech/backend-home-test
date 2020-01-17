
# Chào mừng các bạn đến với công ty Sapo!

Để giúp các bạn đánh giá chính xác năng lực của mình, đồng thời cũng giúp công ty xây dựng kế hoạch sử dụng, phát triển năng lực của các bạn, chúng tôi có một bài kiểm tra năng lực nhỏ.

Dưới đây là mô tả yêu cầu của tính năng: 

## Quản lý thẻ tích điểm của khách hàng


![Loyalty Flow](/flow.png "loyalty flow")


## Mô tả các đối tượng

### Thẻ tích điểm

- Về mặt thực tế, thẻ tích điểm là thứ chủ shop in ra sau đó phát cho người mua.
- Về mặt hệ thống, là đối tượng ghi nhận các thông tin ưu đãi của người mua.
- Thông tin chi tiết:   

|Trường thông tin | Mô tả | Thuộc tính |
|-----------------|-------|------------|
|ID|Số ID của thẻ tích điểm do hệ thống tự sinh ra khi một thẻ tích điểm được khởi tạo thành công | Là trường số <br> Trường thông tin bắt buộc <br> Trường thông tin không được trùng lặp |
|Mã thẻ|Dãy ký tự định danh thẻ tích điểm <br> Thông tin này do client truyền xuống khi tạo thẻ, nếu client không truyền hoặc truyền = null thì hệ thống tự sinh mã theo quy tắc sau <br> ```Lấy 2 ký tự LT ghép với mã id của thẻ``` <br> Ví dụ: LT0001 | Là dãy ký tự thuộc bộ mã code - 128 <br> Độ dài trong khoảng 10-20 ký tự <br> Trường thông tin bắt buộc và không được trùng lặp |
|Số điện thoại khách hàng | Số điện thoại của khách hàng do client truyền xuống khi tạo thẻ | Là trường số thuộc tập từ 0-9 <br> Độ dài trong khoảng 10-25 ký tự <br> Trường thông tin bắt buộc và không được trùng lặp |
|Hạng thẻ|Trường thông tin quy định hạng thẻ <br> Lấy thông tin từ đối tượng hạng thẻ mục 2 <br> Mỗi một thẻ tích điểm chỉ có thể nằm trong 1 hạng thẻ | Trường thông tin không bắt buộc |
|Số điểm | Số điểm tích từ các giao dịch mua hàng | Là trường số <br> Có thể lẻ đến 2 chữ số sau dấu thập phân <br> Có thể âm |
|Doanh thu | Lượng doanh thu tính từ các giao dịch mua hàng | Là trường số <br> Có thể âm |
|Ngày bắt đầu | Ngày bắt đầu dùng được thẻ để giao dịch, tính từ ngày bắt đầu thẻ lên hạng | Trường thời gian |
| Ngày kết thúc | Ngày hết hiệu lực giao dịch của thẻ, tính từ ngày bắt đầu + với thời hạn của hạng thẻ | Trường thời gian |
| Ngày tạo | Ngày tạo thẻ | Trường thời gian |
| Ngày cập nhật | Ngày cập nhật cuối cùng của thẻ | Trường thời gian

<br>
<br>

### Hạng thẻ

- Là trường để phân loại thẻ tích điểm, với các hạng khác nhau, khách hàng sẽ có các ưu đãi riêng.
- Thông tin chi tiết:

|Trường thông tin | Mô tả | Thuộc tính |
|-----------------|-------|------------|
| ID | Số ID của hạng thẻ do hệ thống tự sinh ra khi một thẻ tích điểm được khởi tạo thành công | Là trường số <br> Trường thông tin bắt buộc <br> Trường thông tin không được trùng lặp |
| Tên hạng thẻ | Tên của hạng thẻ <br> Ví dụ : Thẻ bạc, thẻ vàng.. | Là trường text <br> Không bắt trùng <br> Giới hạn tối đa 50 ký tự <br> Trường thông tin bắt buộc |
| Doanh thu lên hạng | Số tiền mà một thẻ tích điểm cần đạt được để lên hạng | Là trường số <br> Giá trị nằm trong khoảng 0 - 9,999,999,999 |
| Thời hạn | Thời hạn hiệu lực của một hạng thẻ | Tính theo ngày. Ví dụ : 100 ngày, 360 ngày. 7 ngày... |
| Chiết khấu % | Ưu đãi cho người mua khi thẻ tích điểm của họ nằm trong hạng này | Là trường số <br> Giá trị nằm trong khoảng 0-100 |
| Ngày tạo | Ngày tạo thẻ | Trường thời gian |
| Ngày cập nhật | Ngày cập nhật cuối cùng của thẻ | Trường thời gian |

<br>
<br>

### Cấu hình

- Thiết lập tỷ lệ quy đổi từ doanh thu ra điểm.
- Thông tin chi tiết:

| Trường thông tin | Mô tả | Thuộc tính |
|-----------------|-------|------------|
| Config | Dùng để quy đổi điểm từ doanh thu mua hàng | 1 điểm = {x} vnđ <br> X là giá trị doanh thu mà người dùng thiết lập <br> Mặc định = 0 | 

<br>
<br>

### Giao dịch tích điểm

- Các giao dịch tăng/ giảm điểm hoặc doanh thu tác động lên thẻ tích điểm của khách hàng.
- Thông tin chi tiết:

| Trường thông tin | Mô tả | Thuộc tính |
|-----------------|-------|------------|
| ID | Số ID của giao dịch do hệ thống tự sinh ra khi một hành động tích điểm được ghi nhận | Là trường số <br> Trường thông tin bắt buộc <br> Trường thông tin không được trùng lặp |
| ID thẻ tích điểm | Đánh dấu cho giao dịch ứng với thẻ tích điểm nào | Là trường thông tin ID do client truyền vào <br> Phải là ID tồn tại trên hệ thống |
| Số điểm điều chỉnh | Số điểm điều chỉnh mà mỗi giao dịch tác động lên thẻ tích điểm <br> Transaction cần dựa vào giá trị doanh thu của client truyền xuống, sau đó check config để quy ra điểm điều chỉnh <br> Ví dụ : + 10, -10... | Là trường số <br> Trường thông tin bắt buộc <br> Giá trị nằm trong khoảng -9,999,999,999 đến 9,999,999,999 |
| Số doanh thu điều chỉnh | Giá trị doanh thu điều chỉnh mà mỗi giao dịch tác động lên thẻ tích điểm <br> Khi doanh thu điều chỉnh tác động lên doanh thu tích điểm của thẻ tích điểm vượt qua các ngưỡng của hạng thẻ thì sẽ cập nhật hạng thẻ ( Có thể lên hạng hoặc xuống hạng ) | Là trường số <br> Trường thông tin bắt buộc <br> Giá trị nằm trong khoảng -9,999,999,999 đến 9,999,999,999 |
| Ngày tạo | Ngày tạo ra bản ghi ghi nhận điểm và doanh thu | Trường thời gian |

<br>
<br>

## Yêu cầu
- Viết API cho phép chỉnh sửa cấu hình tích điểm lưu trữ vào database.   
- Từ dữ liệu đầu vào gồm các thông tin:
    - Thẻ tích điểm của khách hàng
    - Hạng thẻ tích điểm
    - Dữ liệu giao dịch gốc
    - Cấu hình quy đổi điểm

    Xử lý tích điểm vào thẻ cho khách hàng dựa trên giao dịch, thay đổi thông tin hạng thẻ của khách hàng tương ứng   
    Lưu ý: không yêu cầu lưu dữ liệu vào database, tập trung vào xử lý tích điểm, không yêu cầu import dữ liệu từ file excel.
- Viết test với tập dữ liệu mẫu có sẵn.
- Tuỳ chọn trả lời một số câu hỏi bổ sung sau:
    - Nếu giao dịch được tổng hợp từ các hệ thống khác và định kỳ được tải lên hệ thống tích điểm, thì xử lý như thế nào trong trường hợp cấu hình quy đổi điểm bị thay đổi giữa các lần giao dịch của khách hàng.    
    VD: Khách hàng có 3 giao dịch mua hàng vào buổi sáng, và 2 giao dịch vào buổi chiều cùng ngày. Cấu hình quy đổi điểm được thay đổi vào 12h trưa ngày hôm đó. 22h cuối ngày thì dữ liệu mới được tổng hợp về hệ thống tích điểm.
    - Để tăng hiệu năng hệ thống khi có rất nhiều giao dịch của nhiều khách hàng đồng thời thì có giải pháp nào không?

### Lưu ý:
- Nếu bạn dùng mysql/sql server/postgresql,v..v... xin hãy gửi cho chúng tôi schema của bạn.
- Bạn vui lòng mô tả chúng tôi biết từng bước để chạy được từng ý của bài tập.
- Đẩy dự án lên Git và gửi đường link cho chúng tôi theo địa chỉ interviewer.tech@sapo.vn
