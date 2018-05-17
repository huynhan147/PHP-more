# **Clean code PHP**
- *Biến* :
 - Sử dụng tên biến có ý nghĩa và dễ hiểu : `ví dụ : $name thay vì $n`
 - Đặt tên sao cho dễ tìm kiếm
 - Sử dụng các biến có tính giải thích rằng biến đó lưu giá trị về cái gì
 - Tránh lồng điều kiện quá nhiều và nên return sớm
 - Sử dụng đối số mặc định thay vì phải kiểm tra bằng biểu thức điều kiện
- *Hàm* :
 - Đối số của hàm nên ít hơn hoặc bằng 2
 - Hàm chỉ nên thực hiện một chức năng
 - Tên hàm nên thể hiện chức năng của nó 
 - Không nên sử dụng cờ như là một đối số truyền vào hàm
 - Tránh dùng điều kiện phủ định
 - Xóa những code không cần thiết
# **Các chuẩn PSR trong php**
- *PSR-1: Chuẩn viết code cơ bản* : 
 - Trong file cần sử dụng thẻ <?php ?> hoặc <?= ?>
 - Kiểu mã hóa code sử dụng UTF-8
 - Namespace và class cần theo chuẩn "autoload" PSR
 - Biến constant cần được khai báo bằng chữ in hoa và cách nhau bởi dấu `_`
 - Phương thức cần được khai báo theo kiểu cameCase (nameFunction)
- *PSR-2 : Tiêu chuẩn trình bày code*
 - Phải tuân  thủ PSR-1
 - Sử dụng 4 ký tự space để lùi khối()
 - Mỗi dòng code dưới 120 ký tự , nên dưới 80 ký tự
 - Phải có dòng trắng sau namespace và dòng trắng sau mỗi khối code
 - Ký tự `{` và `}` phải ở một dòng riêng đối với class và function
 - Phải có khoảng trắng sau `if,elseif else`
 - Hằng số `true,false,null` phải viết thường
 - Từ khóa `extends` và `implements` phải cùng dùng với `class`
- *PSR-3 : Giao diện logger*
 - Mọi method chỉ chấp nhận 1 string tin nhắn
 - Tên placeholders phải phù hợp với key log
 - Tên placeholders phải được phân cách bằng dấu ngoặc nhọn `{` và dấu `}`
 - Không được chứa bất kỳ khoảng trắng giữa các ký tự tên placeholders
- *PSR-4 :Tiêu chuẩn về tự động nạp*
 - Namespace đầy đủ phải có 1 namespace gốc
 - Phải có một hoặc nhiều namespace con
 - Phải có một tên lớp kết thúc (Classname)
`\<NamespaceName>\<SubNamespaceNames>\<ClassName>`
# **Nguyên tắc SOLID** :
- S -RP: Nguyên tắc chịu trách nhiệm duy nhất : Một class nên giữ một trách nhiệm duy nhất
- O -CP: Nguyên tắc đóng mở : Có thể thoải mái mở rộng class, không được sửa đổi bên trong class đó : Nên viết class mới mở rộng class cũ bằng cách kế thừa class cũ, không nên sửa đổi class cũ
- L -SP: Nguyên tắc thay thế Liskov : các Object của clas con có thể thay thế class cha mà không làm thay đổi tính đúng đắn của chương trình
- I -SP: Nguyên tắc phân đoạn giao diện : Thay vì dùng 1 interface lớn, ta nên tách thành nhiều interface nhỏ, với nhiều mục đích cụ thể
- D -IP: Nguyên tắc đảo ngược phụ thuộc : Các module cấp cao không nên phụ thuộc vào module cấp thấp. cả 2 nên phụ thuộc vào abstraction


