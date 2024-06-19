# QL_Tai_Khoan_Game
Bài tập lớn hệ quản trị cơ sở dữ liệu.Với ứng dụng :Quản lý tài khoản,Quản lý thông tin nhân vật,Quản lý lịch sử hoạt động.
## Bài toán : Quản lý tài khoản game 
+ Họ và tên: Trần Chiến Thắng
+ MSSV: K215480106121
+ Lớp:K57KMT01
## Mô tả bài toán
* Các chức năng

+ Quản lý tài khoản: Gồm các thuộc tính tên đăng nhập,mật khẩu,ngày tạo tài khoản,lần đăng nhập cuối cùng.
Có các chức năng thêm, sửa, xóa ,liệt kê theo tên đăng nhập,Đổi mật khẩu 1 tài khoản,check login cho 1 tài khoản.
+ Quản lý thông tin nhân vật: Có các chức năng thêm, sửa, xóa, liệt kê theo profile_id .
+ Quản lý lịch sử hoạt động: Có các chức năng thêm, sửa, xóa, liệt kê theo user_id.
  
* Báo cáo
+ Báo cáo số người dùng được tạo trong tháng
  - Truy vấn để đếm số người dùng được tạo trong tháng
  ```sql
    SELECT COUNT(*) AS TotalUsersCreated
    FROM nguoidung
    WHERE MONTH(ngaytaoTk) = @CurrentMonth
      AND YEAR(ngaytaoTk) = @CurrentYear;
END;
+ Báo cáo danh sách các hoạt động của tài khoản trong tháng
  - Truy vấn này sẽ liệt kê danh sách các hoạt động tài khoản đã được ghi lại trong tháng cụ thể.
    ![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/7f26cd70-a853-46a6-9aeb-5e1cb135d777)
+ Báo cáo số lượng người dùng đã được tạo trong tháng hiện tại
  - Truy vấn này sẽ đếm số lượng người dùng đã được tạo trong tháng hiện tại.
    ![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/777d4f5d-501e-4d5c-90cf-8dc85d9b007a)
+ Báo cáo danh sách các người dùng được tạo trong tháng hiện tại
  - Truy vấn này sẽ liệt kê danh sách các người dùng được tạo trong tháng hiện tại.
    ![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/b37dd712-8be2-44d4-96e7-1bba48667ef4)
+ Báo cáo số lượng người dùng được tạo trong từng ngày của tháng hiện tại
  - Truy vấn này sẽ đưa ra báo cáo số lượng người dùng được tạo trong từng ngày của tháng hiện tại.
    ![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/4384275b-5984-4722-98e9-aa82d9e082f6)
* Các bảng của hệ thống
- nguoidung(#user_id,@Tendangnhap,@Matkhau,@Email,@NgaytaoTK,@Landangnhapcuoi,@TrangthaiTK)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/bb3dd31d-2e92-46ab-9590-a5e4b2b3b9db)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/8e3fe189-fa97-436d-980a-af3cb652c036)
- Bảng nguoidung:
+ Các trường:
  - user_id (INT): Primary Key (PK). Đây là một số duy nhất cho mỗi người dùng.
  - Tendangnhap (NVARCHAR(100)): Candidate Key. Là tên đăng nhập duy nhất.
  - Matkhau (NVARCHAR(255)): Mật khẩu được mã hóa (ví dụ: SHA2_256).
  - Email (NVARCHAR(100)): Địa chỉ email của người dùng.
  - NgaytaoTk (DATE): Ngày tạo tài khoản, có thể NULL nếu không có thông tin.
  - Landangnhapcuoi (DATETIME): Thời điểm đăng nhập cuối cùng.
  - Capnhatluc (DATETIME): Thời điểm cập nhật thông tin người dùng.
+ Ràng buộc dữ liệu:
  - user_id: PK không được NULL, và giá trị duy nhất.
  - Tendangnhap: Candidate Key, không được NULL và duy nhất.
  - Matkhau: Bắt buộc nhập.
  - Email: Có thể NULL.
  - NgaytaoTk, Landangnhapcuoi, Capnhatluc: Có thể NULL tùy thuộc vào nhu cầu.
+ Giải thích:
  - user_id là PK để xác định duy nhất mỗi người dùng.
  - Tendangnhap là Candidate Key để xác định duy nhất mỗi tên đăng nhập.
  - Matkhau được yêu cầu bắt buộc nhập để đảm bảo tính bảo mật.
  - Email có thể NULL vì người dùng có thể không cung cấp địa chỉ email.
  - NgaytaoTk, Landangnhapcuoi, Capnhatluc là các trường thời gian có thể NULL nếu không có thông tin hoặc chưa cập nhật.
- thongtinnhanvat(#profile_id,@user_id,@TenNV,@Capdo,@EXP,@Vip,@Danhhieu,@Tiendanap,@Tiendadung,@Capnhatluc)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/30e04e67-d0a0-44f5-914c-f4484702d371)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/786325c8-0565-4525-80d7-1107a74b46ad)
-Bảng lichsuhoatdong
+ Các trường:
  - log_id (INT): Primary Key (PK). Đây là một số duy nhất cho mỗi log hoạt động.
  - user_id (INT): Foreign Key (FK) tham chiếu đến nguoidung(user_id). Xác định người dùng thực hiện hoạt động.
  - Loaihoatdong (NVARCHAR(50)): Loại hoạt động được thực hiện.
  - ChitietHD (NVARCHAR(250)): Chi tiết về hoạt động.
  - Thoigian (DATETIME): Thời điểm hoạt động được thực hiện.
+ Ràng buộc dữ liệu:
  - log_id: PK không được NULL và duy nhất.
  - user_id: FK để liên kết với bảng nguoidung(user_id).
  - Loaihoatdong, ChitietHD, Thoigian: Các trường này có thể NULL hoặc không tùy thuộc vào nhu cầu cụ thể của ứng dụng.
+ Giải thích:
  - log_id là PK để xác định duy nhất mỗi log hoạt động.
  - user_id là FK để liên kết log hoạt động với người dùng tương ứng.
  - Loaihoatdong và ChitietHD là các trường lưu trữ văn bản, còn Thoigian là trường thời gian để lưu lại thời điểm hoạt động được thực hiện.
- Bảng thongtinnhanvat
+ Các trường:
  - profile_id (INT): Primary Key (PK). Đây là một số duy nhất cho mỗi thông tin nhân vật.
  - user_id (INT): Foreign Key (FK) tham chiếu đến nguoidung(user_id). Xác định người dùng liên quan đến thông tin nhân vật.
  - TenNV (NVARCHAR(100)): Tên của nhân vật.
  - Capdo (INT): Cấp độ của nhân vật.
  - EXP (FLOAT): Kinh nghiệm tích lũy của nhân vật.
  - Vip (INT): Mức độ VIP của nhân vật.
  - Danhhieu (NVARCHAR(50)): Danh hiệu của nhân vật.
  - Tiendanap (NVARCHAR(50)): Số tiền đã nạp vào tài khoản của nhân vật.
  - Tiendadung (NVARCHAR(50)): Số tiền đã sử dụng của nhân vật.
  - Capnhatluc (DATETIME): Thời điểm cập nhật thông tin nhân vật.
+ Ràng buộc dữ liệu:
  - profile_id: PK không được NULL và duy nhất.
  - user_id: FK để liên kết với bảng nguoidung(user_id).
  - TenNV, Capdo, EXP, Vip, Danhhieu, Tiendanap, Tiendadung: Các trường này có thể NULL hoặc không tùy thuộc vào nhu cầu cụ thể của ứng dụng.
+ Giải thích:
  - profile_id là PK để xác định duy nhất mỗi thông tin nhân vật.
  - user_id là FK để liên kết thông tin nhân vật với người dùng tương ứng.
  - Các trường như Capdo (INT), EXP (FLOAT), Capnhatluc (DATETIME) được sử dụng cho các giá trị số học, tiền tệ và thời gian, phù hợp với nhu cầu lưu trữ và tính toán trong ứng dụng.
- lichsuhoatdong(#log_id,@user_id,@Loaihoatdong,@ChitietHD,@Thoigian)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/25dfe783-0e35-408d-af29-1be539c63d23)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/b57ca008-b602-4459-86b5-8ab06e844463)

* Các SP Cho các chức năng ở trên
- Chức năng thêm các thuộc tính theo tên đăng nhập
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/4819f001-3c7f-4ee7-908d-7181d552552d)
- Chức năng xóa các thuộc tính theo tên đăng nhập
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/091660aa-1891-44a3-9802-e504a77da9eb)
- Chức năng check login
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/a74d7d8d-a364-4b64-bfe8-07b6e6c6faef)
- Báo cáo số người dùng được tạo trong tháng
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/70954bd8-31ab-490d-bf9e-cf8b62383daa)
- Báo cáo danh sách các hoạt động của các tài khoản trong tháng
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/45829ebb-6fb6-477f-b09b-e6cb37b420d8)

*Curson: 
+ Procedure ListUsersAndProfiles sử dụng một cursor (curUsers) để duyệt qua danh sách các người dùng trong bảng nguoidung và thông tin nhân vật tương ứng từ bảng thongtinnhanvat.
Các thông tin của từng người dùng và thông tin nhân vật sẽ được in ra màn hình bằng câu lệnh PRINT.
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/d25198d5-47fd-422c-a97b-abb16a727570)

*Trigger:
+ Trigger sẽ được kích hoạt sau khi một người dùng (nguoidung) được xóa. Khi người dùng bị xóa, trigger này sẽ tự động xóa thông tin nhân vật (character profile) của người dùng đó từ bảng thongtinnhanvat và lịch sử hoạt động (activity log) của người dùng đó từ bảng lichlichsuhoatdong.
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/69cf82ae-0456-48ab-a8b4-9f4eff03ece3)
+ Trigger trgUpdateNgaytaoTk sẽ được kích hoạt sau khi có sự kiện INSERT vào bảng nguoidung.
Nó lấy ngày giờ hiện tại bằng GETDATE() và cập nhật giá trị ngaytaoTk cho người dùng vừa được thêm vào.
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/041524de-63fa-4885-9555-f4a9c2fd359e)


##### 
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/b85b5df1-36b5-41a4-8a6c-39dff70633b2)









