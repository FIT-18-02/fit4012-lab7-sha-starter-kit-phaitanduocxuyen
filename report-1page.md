# FIT4012 Lab 7 - Báo cáo 1 trang: SHA-256

## 1. Mục tiêu / Objective

Bài thực hành nhằm mục tiêu tìm hiểu và phân tích nguyên lý hoạt động cốt lõi của thuật toán băm mật mã học SHA-256. Qua đó, áp dụng thuật toán vào các bài toán thực tế trong an toàn thông tin bao gồm: kiểm tra tính toàn vẹn của dữ liệu/file, cơ chế băm mật khẩu cơ bản và cải tiến độ an toàn bằng kỹ thuật thêm muối (Salt).

## 2. Cách làm / Approach

Em đã tiến hành thực hiện bài thực hành theo các bước sau:
- Sử dụng trình biên dịch tích hợp trên CLion để build mã nguồn dự án thành các file chạy thực thi.
- Chạy kiểm thử hàm băm SHA-256 cốt lõi thông qua chế độ tự kiểm tra (--self-test) với các chuỗi mẫu tiêu chuẩn quốc tế.
- Thực hiện kiểm tra tính toàn vẹn file bằng cách so sánh mã băm trước và sau khi file bị chỉnh sửa (tampered).
- Triển khai băm mật khẩu thông thường và kiểm thử tính năng đăng nhập đúng/sai.
- Thử nghiệm cơ chế băm mật khẩu có muối (Salted) để chứng minh tính năng chống tấn công bảng băm tính sẵn.

## 3. Kết quả / Result

Điền minh chứng chính:

- Hash của chuỗi `abc`: ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad
- Hash của file mẫu trước khi sửa: 5ee62dc925a9958dbd6732c570a23c7f65a8c11066e889b15068cfb4bf1a0bd9
- Kết quả kiểm tra file sau khi sửa nội dung: c232e5627e703ee5b311e0df8520b3d10dc8867b27636bb58fe58eb1fb9d6acb (Hệ thống phát hiện lỗi và báo [FAIL])
- Kết quả đăng nhập với mật khẩu đúng: [PASS] Login success
- Kết quả đăng nhập với mật khẩu sai: [FAIL] Login failed: wrong password
- Hai bản ghi `salt:hash` của cùng một mật khẩu có giống nhau không? Không giống nhau (Do chuỗi Salt ngẫu nhiên được sinh ra khác nhau ở mỗi lần đăng ký).

## 4. Kết luận / Conclusion

- SHA-256 giúp phát hiện thay đổi dữ liệu thông qua hiệu ứng thác đổ (Avalanche Effect) — chỉ cần thay đổi một ký tự nhỏ, mã băm đầu ra sẽ biến đổi hoàn toàn, giúp phát hiện ngay lập tức hành vi chỉnh sửa trái phép.
- Cần sử dụng Salt khi lưu mật khẩu để đảm bảo rằng cùng một mật khẩu của các người dùng khác nhau sẽ sinh ra các chuỗi băm khác nhau trong cơ sở dữ liệu, từ đó vô hiệu hóa đòn tấn công bằng bảng băm tính sẵn (Rainbow Table).
- Thuật toán SHA-256 demo trong bài lab chưa nên dùng trực tiếp cho hệ thống xác thực thật vì tốc độ tính toán của SHA-256 quá nhanh trên phần cứng hiện đại, khiến kẻ tấn công dễ dàng thực hiện dò quét mật khẩu (Brute-force). Hệ thống thật nên dùng các thuật toán băm mật khẩu chuyên dụng có cơ chế làm chậm như bcrypt, Argon2id hoặc scrypt.