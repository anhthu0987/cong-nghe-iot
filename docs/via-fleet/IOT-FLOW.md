# Hợp đồng giao diện VIA Fleet với IOT

Nguồn: frontend/urls.py, frontend/views.py, frontend/forms.py,
violations/views.py, FRONTEND.md. Chỉ đổi giao diện, không thêm nghiệp vụ.

| Route | Màn / quyền |
|---|---|
| /login/ | Đăng nhập bằng username, mật khẩu; vai trò theo tài khoản |
| /register/ | Chỉ tạo tài xế; tự đăng nhập rồi chuyển /profile/ |
| /dashboard/ | Admin 4 chỉ số; tài xế 3 chỉ số và dữ liệu của mình |
| /profile/ | Hồ sơ cá nhân, một ảnh mặt; /face/ là alias |
| /license/ | GPLX, hệ hạng, hai ảnh, ngày cấp/hết hạn |
| /drivers/ | Admin: tìm họ tên/điện thoại/username; lọc hồ sơ |
| /drivers/<id>/ | Admin: thông tin, GPLX, khuôn mặt, duyệt hồ sơ |
| /vehicles/ | Admin quản lý; tài xế chỉ xem xe được giao còn hiệu lực |
| /assignments/ | Admin: danh sách và thêm/sửa phân công |
| /sessions/ | Chỉ đọc, admin toàn bộ / tài xế của mình |
| /violations/ | Admin toàn bộ / tài xế của mình chỉ PENDING, APPROVED |
| /violations/<id>/ | Admin duyệt; tài xế chỉ đọc, không lịch sử nội bộ |
| /devices/ | Admin quản lý thiết bị |
| /catalogs/ | Admin thêm/sửa/xóa nhiều loại xe chưa được dùng |
| /violation-types/ | Admin thêm/sửa; không xóa |
| /password/change/ | Đổi mật khẩu, giữ phiên hiện tại |
| /logout/ | POST đăng xuất |

Thêm/sửa: /manage/<key>/new/ và /manage/<key>/<id>/.
Key: vehicles, catalogs, assignments, devices, violation-types.
Các danh sách phân trang 20 bản ghi; bộ lọc trạng thái chỉ ở những entity
có status được backend hỗ trợ. Tổng quan chỉ 10 phiên gần nhất, không phân trang.

## Ràng buộc

- Không bộ chuyển vai trò. Admin = role ADMIN hoặc superuser, không chỉ is_staff.
- Không nút tạo tài xế; tài xế tự đăng ký.
- Không trang chi tiết/sửa/xóa phiên, không bắt đầu/kết thúc phiên trên web.
- Không GPS, doanh thu, quãng đường, livestream, chuông thông báo giả hoặc realtime.
- Dashboard không thêm tỷ lệ tải, tăng trưởng hay số xe bảo dưỡng.
- GPLX hết hạn khi expiry_date <= hôm nay. Duyệt hồ sơ tổng thể chỉ khi đủ
  thông tin, GPLX đã duyệt còn hạn, khuôn mặt đã duyệt có dữ liệu nhận diện.
- PENDING ưu tiên hơn INCOMPLETE khi GPLX hoặc ảnh đang chờ duyệt.
- Hồ sơ/GPLX/duyệt có version, dữ liệu thay đổi phải tải lại trước khi lưu.
- Ảnh JPG/PNG/WebP, tối đa 5MB và 20 megapixel; không nhập vector thủ công.
- GPLX lần đầu đủ hai ảnh, lần sau có thể thay một ảnh; cập nhật cần duyệt lại.
- Đổi điện thoại/địa chỉ không mặc định yêu cầu duyệt lại; đổi ảnh cần duyệt.
- Không xóa xe/phân công/lịch sử. Xe có ACTIVE/INACTIVE/LIQUIDATED.
- Phân công đã có phiên khóa tài xế, xe, bắt đầu; chỉ cập nhật kết thúc.
- Kết thúc ngay chỉ khi đang hiệu lực; vẫn được kết thúc khi tài xế/xe không
  còn đủ điều kiện; không tự kết thúc phiên lái.
- Một thiết bị/xe; không chuyển thiết bị khỏi xe có phiên đang lái.
- Vi phạm chỉ PENDING mới chỉnh loại/mức độ/ghi chú và xác nhận/từ chối.
  Xác nhận cần ít nhất một Evidence và toàn bộ metadata hợp lệ (URL HTTPS).
  Không tự tải URL để khẳng định nội dung bằng chứng.
- Xem xét lại chỉ khi chưa có kháng cáo. Kháng cáo chưa triển khai.
- Không tạo vi phạm hoặc upload bằng chứng thủ công trên web.
- Loại xe đang dùng không xóa, không đổi nhóm. Kết quả xóa nhiều gồm cả
  thành công và bản ghi bị bảo vệ.

## Cài đặt đã kiểm tra

Gemini CLI 0.66.0. Sáu skill enabled trong C:/Users/Admin/.gemini/skills:
generate-design, manage-design-system, upload-to-stitch, taste-design,
enhance-prompt, design-md. Nguồn: google-labs-code/stitch-skills.
Gemini CLI chưa có MCP server cấu hình; đăng nhập Stitch trên Chrome
không đồng nghĩa Gemini CLI đã xác thực Stitch MCP.
