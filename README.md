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
    -- Truy vấn để đếm số người dùng được tạo trong tháng
    SELECT COUNT(*) AS TotalUsersCreated
    FROM nguoidung
    WHERE MONTH(ngaytaoTk) = @CurrentMonth
      AND YEAR(ngaytaoTk) = @CurrentYear;
END;
+ Báo cáo danh sách các hoạt động của tài khoản trong tháng
    --Truy vấn này sẽ liệt kê danh sách các hoạt động tài khoản đã được ghi lại trong tháng cụ thể.
    SELECT user_id, Loaihoatdong, ChitietHD, Thoigian
    FROM lichsuhoatdong
    WHERE MONTH(Thoigian) = MONTH(GETDATE())
      AND YEAR(Thoigian) = YEAR(GETDATE())
    ORDER BY Thoigian DESC;
+ Báo cáo số lượng người dùng đã được tạo trong tháng hiện tại
    --Truy vấn này sẽ đếm số lượng người dùng đã được tạo trong tháng hiện tại.
    SELECT COUNT(*) AS TotalUsersCreated
    FROM nguoidung
    WHERE MONTH(ngaytaoTk) = MONTH(GETDATE())
      AND YEAR(ngaytaoTk) = YEAR(GETDATE());
+ Báo cáo danh sách các người dùng được tạo trong tháng hiện tại
    --Truy vấn này sẽ liệt kê danh sách các người dùng được tạo trong tháng hiện tại.
      SELECT user_id, Tendangnhap, ngaytaoTk
    FROM nguoidung
    WHERE MONTH(ngaytaoTk) = MONTH(GETDATE())
      AND YEAR(ngaytaoTk) = YEAR(GETDATE())
    ORDER BY ngaytaoTk DESC;
+ Báo cáo số lượng người dùng được tạo trong từng ngày của tháng hiện tại
    --Truy vấn này sẽ đưa ra báo cáo số lượng người dùng được tạo trong từng ngày của tháng hiện tại.
    SELECT DAY(ngaytaoTk) AS Ngay,
           COUNT(*) AS SoLuongNgDung
    FROM nguoidung
    WHERE MONTH(ngaytaoTk) = MONTH(GETDATE())
      AND YEAR(ngaytaoTk) = YEAR(GETDATE())
    GROUP BY DAY(ngaytaoTk)
    ORDER BY Ngay;
+ Báo cáo số lượng hoạt động của từng tài khoản đã được ghi lại trong tháng cụ thể
    --Truy vấn này sẽ đếm số lượng hoạt động tài khoản đã được ghi lại trong tháng cụ thể.
    SELECT COUNT(*) AS TotalActivities
    FROM lichsuhoatdong
    WHERE MONTH(Thoigian) = MONTH(GETDATE())
      AND YEAR(Thoigian) = YEAR(GETDATE());

* Các bảng của hệ thống
- nguoidung(#user_id,@Tendangnhap,@Matkhau,@Email,@NgaytaoTK,@Landangnhapcuoi,@TrangthaiTK)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/bb3dd31d-2e92-46ab-9590-a5e4b2b3b9db)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/8e3fe189-fa97-436d-980a-af3cb652c036)
- thongtinnhanvat(#profile_id,@user_id,@TenNV,@Capdo,@EXP,@Vip,@Danhhieu,@Tiendanap,@Tiendadung,@Capnhatluc)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/30e04e67-d0a0-44f5-914c-f4484702d371)
![image](https://github.com/thangtran1904/QL_Tai_Khoan_Game/assets/168847723/786325c8-0565-4525-80d7-1107a74b46ad)
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









