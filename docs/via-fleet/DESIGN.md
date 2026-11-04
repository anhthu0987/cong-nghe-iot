# VIA Fleet — Navy & Blue

Vững tay lái, trọn hành trình.

## Phạm vi

Thiết kế lại phần trình bày của dự án IOT/SaveLife. Giữ nguyên routes, nghiệp vụ,
trường dữ liệu, validation và phân quyền Django. Không thay đổi backend.
Đối chiếu frontend/urls.py, frontend/views.py, frontend/forms.py,
violations/views.py và FRONTEND.md ngày 04/11/2026.

## Nhận diện

Logo chữ V kết hợp đường đi. Giao diện vận hành gọn gàng, mật độ vừa phải,
ưu tiên đọc bảng và hoàn thành biểu mẫu. Không landing page, gradient lớn,
hiệu ứng kính hay hiệu ứng chuyển động liên tục.

## Màu sắc

| Vai trò | Màu |
|---|---|
| Primary / mục menu được chọn | #2563EB |
| Hover primary | #1D4ED8 |
| Sidebar | #0F172A |
| Chữ sidebar chính | #F8FAFC |
| Chữ phụ / icon sidebar | #CBD5E1 |
| Chữ / icon mục đang chọn | #FFFFFF |
| Accent phụ, dùng tiết chế | #0891B2 |
| Nền trang | #F1F5F9 |
| Card / biểu mẫu / header | #FFFFFF |
| Chữ chính | #0F172A |
| Chữ phụ | #64748B |
| Viền | #E2E8F0 |
| Tiêu đề bảng | #F8FAFC |
| Hàng hover | #EFF6FF |

| Trạng thái | Chữ | Nền |
|---|---|---|
| Thành công | #166534 | #DCFCE7 |
| Chờ xử lý | #854D0E | #FEF9C3 |
| Lỗi / nguy hiểm | #B91C1C | #FEE2E2 |
| Thông tin | #1D4ED8 | #DBEAFE |
| Trung tính | #475569 | #F1F5F9 |

Trạng thái luôn có nhãn chữ. Không sử dụng lại xanh cổ vịt/cam đất.

## Typography, khoảng cách và thành phần

Be Vietnam Pro, fallback sans-serif hỗ trợ tiếng Việt. Body 14–16px,
tiêu đề trang 28–32px, tiêu đề card 18px; số liệu dùng tabular numerals.
Thang khoảng cách 4/8/12/16/24/32px. Card bo 12–16px, bóng nhẹ.
Sidebar desktop khoảng 240px, header trắng khoảng 72px, padding nội dung 32px.
Nút chính xanh dương chữ trắng; nút phụ trắng viền xám chữ navy;
nút nguy hiểm đỏ. Icon nét mảnh đồng nhất, không dùng emoji.
Input có label trên, lỗi ngay dưới, focus viền xanh và vòng sáng nhẹ.
Card chỉ số trắng, icon trên ô xanh nhạt. Không tô xanh toàn card.

## Bố cục và responsive

Desktop thiết kế 1440px. Trang chi tiết hai cột: thông tin trái,
trạng thái và hành động phải. Tài xế có giao diện 390px: menu thu gọn,
biểu mẫu một cột, bảng đổi thành card, vùng chạm tối thiểu 44px.
Không tràn ngang trên mobile. Tôn trọng prefers-reduced-motion.

## Quy tắc tương tác

Loading, danh sách trống, không có kết quả, lỗi trường, lưu thành công,
modal xác nhận, xung đột phiên bản yêu cầu tải lại và trang 403.
Không đặt nút giả chỉ để trang trí. Liên kết phải đúng màn và vai trò.
Ngày dd/mm/yyyy, giờ 24h. Dữ liệu và ảnh mẫu được ghi rõ minh họa.

## Dự án Stitch

https://stitch.withgoogle.com/projects/1122113802084360174

Design system tương ứng đã có: Fleet Dispatch Operating System.
Không dùng Intelligent Fleet Telematics (cyan chính và điểm nhấn cam).
