# 5.Yêu cầu đầu ra
1. Phần I.Phân tích bài toán(I/O)
- Input:\
          - Ban Kỹ thuật (3 người): Viết code, test API, quản lý mã nguồn.\
            Ban Thiết kế (2 người): Thiết kế UI, tạo tài sản đồ họa.\
            Ban Kinh doanh (2 người): Viết Business Plan, liên hệ đối tác.\
            Nhà đầu tư tiềm năng (1 người, bên ngoài): Cần xem được business plan và slide pitch.\
            - Tài liệu chứa dữ liệu nhạy cảm (API keys, thông tin khách hàng) chỉ Restricted, tuyệt đối không Anyone with link.\
              Tài liệu làm chung (slide pitch, business summary) dễ chia sẻ giữa các ban nhưng vẫn kiểm soát được quyền sửa.\
              Tất cả tài liệu quan trọng phải được lưu trên Cloud để chứa Version History tối thiểu 30 ngày.\
              Quyền nhà đầu tư phải tự động hết hạn sau 14 ngày (Expiration Date).

- Output: \
          - Cấu trúc thư mục phân cấp rõ ràng theo phòng ban và dự án\
          - Bảng phân quyền hoàn chỉnh, chi tiết cho từng vai trò trong nhóm
          - Xử lý tình huống ghi gặp rủi ro\


Phần I.2.Đề xuất giải pháp

```
CampusPay (Cấp 1: Thư mục gốc)
|
|-- 1.General & Management (Cấp 2: Quản lý dự án chung)
|   |_Biên bản cuộc họp và lịch làm việc
|   |_Quy trình vận hành và bảo mật
|
|-- 2. Tech (Cấp 2: Ban Kỹ Thuật)
|   |_Mã nguồn dự án
|   |_API keys, thông tin khách hàng
|
|-- 3. Design UI & UX(Cấp 2: Ban Thiết kế)
|   |_Thiết kế UI
|   |_Tạo tài sản đồ họa
|
|-- 4. Business (Cấp 2: Ban kinh doanh)
|   |_Viết Business Plan  
|   |_Liên hệ đối tác
|
|-- 5.Partnership (Cấp 2: Nhà đầu tư tiềm năng)
    |_Cần xem được business plan và slide pitch

```
Phần I.3.Thiết kế các bước
- Bước 1: Tạo cây thư mục
- Bước 2: Cấu hình theo bảo mật gốc
- Bước 3: Cấp quyền theo ban
- Bước 4: Cấu hình chia sẻ
- Bước 5: Kiểm tra
- Bước 6: Vận hành
2. Phần II.Triển khai chống lỗi

|Loại tài liệu|Ban kỹ thuật|Ban thiết kế|Ban kinh doanh|Nhà đầu tư|Ghi chú bảo mật
|-|-|-|-|-|-|
Mã nguồn|Editor|No access|No access|No access|Không dùng link chung
Tài sản đồ họa|Viewer|Editor|Viewer|Viewer|Xem sản phẩm
Khách hàng|Commenter|Viewer|Editor|Editor|Nhà đầu tư có giới hạn truy cập
Slide pitch|Viewer|Editor|Editor|Editor|Cho phép nhà đầu tư tải file thuyết trình
Tài liệu chung dự án|Viewer|Viewer|Viewer|Viewer|Tài liệu hành chính, tiến độ của nhóm

- Bẫy 1:
  - Quyền: Commenter
  - Tùy chọn: Tắt tính năng download/copy
  - Lý do: Để bảo mật dữ liệu
- Bẫy 2:
  - Quyền: Viewer
  - Tùy chọn: Để tính năng download
  - Lý do: Thuận tiện trong việc tải xuống và sử dụng sản phẩm để thuyết trình
- Bẫy 3:
  - Bước 1: Xóa khỏi danh sách chia sẻ 
  - Bước 2: Xóa tài khoản khỏi nhóm