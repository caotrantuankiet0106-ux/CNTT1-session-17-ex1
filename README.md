# [N26DTCN050]_[Nhập Môn Công Nghệ Thông Tin]_Session17_Bài 1

## Phần 1: Phân tích lập luận của Nam

Lập luận của Nam: *"DNS Lookup không tìm thấy địa chỉ IP nên máy mới báo lỗi 500. Em cần đổi DNS sang 8.8.8.8 để vào lại trang web"* là **hoàn toàn sai**:

1. **Sai về lỗi DNS:** 
   * Lỗi DNS hoặc mất mạng sẽ trả về các mã như `ERR_NAME_NOT_RESOLVED` hoặc `NXDOMAIN`, hoàn toàn không thể sinh ra lỗi `500 Internal Server Error`.
2. **Sai về mã trạng thái HTTP:**
   * Mã `500 Internal Server Error` (thuộc nhóm 5xx) chứng tỏ **request đã vượt qua toàn bộ quá trình DNS và kết nối mạng thành công** để đến được server.
   * Lỗi 500 phát sinh **hoàn toàn ở phía Server** (lỗi code backend, sập kết nối database, quá tải), không liên quan đến cấu hình DNS hay đường truyền của client. Việc Nam gọi thợ sửa mạng hay đổi sang DNS `8.8.8.8` là vô ích.

---

## Phần 2: Sơ đồ luồng dữ liệu HTTP Request

```text
[1. User nhập URL] ---> [2. DNS Lookup] ---> [3. Thiết lập TCP/TLS] ---> [4. Gửi HTTP Request] ---> [5. Server Xử lý & Phản hồi (Lỗi 500)]