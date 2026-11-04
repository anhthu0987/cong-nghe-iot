# VIA Fleet — đặc tả thiết kế đã hợp nhất

Ưu tiên cao nhất: giữ y hệt luồng và quyền của dự án IOT; chỉ thay nhận diện và giao diện. Đọc IOT-FLOW.md và DESIGN.md cùng thư mục. Khi đặc tả khác code IOT, đối chiếu code, không tự thêm chức năng. Đây là thiết kế UI, dữ liệu mẫu không ghi vào database thật.

Thiết kế lại giao diện web quản lý vận tải và giám sát tài xế với tên mới “VIA Fleet”.

Đây là ứng dụng nghiệp vụ cho một công ty vận tải, có hai vai trò: Quản trị viên và Tài xế. Hãy tạo một hệ thống màn hình liên kết với nhau, giữ chính xác các luồng và quyền được mô tả dưới đây.

Toàn bộ nội dung giao diện bằng tiếng Việt có dấu, tự nhiên, rõ ràng. Thiết kế ở mức chi tiết cao, có dữ liệu mẫu thực tế, có thể dùng làm bản thiết kế để triển khai trên Django.

1. NHẬN DIỆN VÀ PHONG CÁCH

Tên ứng dụng: VIA Fleet.
Thông điệp: “Vững tay lái, trọn hành trình.”
Logo đơn giản kết hợp chữ V và đường đi.

Bảng màu duy nhất (thay toàn bộ bảng màu cũ):
- Chính #2563EB; hover #1D4ED8.
- Sidebar #0F172A; chữ chính #F8FAFC; chữ phụ/icon #CBD5E1.
- Menu đang chọn #2563EB, chữ/icon #FFFFFF.
- Cyan phụ #0891B2, dùng tiết chế.
- Nền #F1F5F9; card/form/header #FFFFFF.
- Chữ chính #0F172A; chữ phụ #64748B; viền #E2E8F0.
- Thành công #166534 / #DCFCE7; chờ #854D0E / #FEF9C3.
- Lỗi/nguy hiểm #B91C1C / #FEE2E2; thông tin #1D4ED8 / #DBEAFE.
- Trung tính #475569 / #F1F5F9.
- Header bảng #F8FAFC; hàng hover #EFF6FF.
- Input focus viền xanh, vòng sáng nhẹ; nút phụ trắng viền xám chữ navy.
- Không gradient lớn; card trắng, icon chỉ trên ô nền xanh nhạt.
- Trạng thái luôn có chữ.
Phong cách gọn gàng, chuyên nghiệp, thân thiện, phù hợp phần mềm vận hành.
Dùng font Be Vietnam Pro hoặc font hỗ trợ tiếng Việt tốt.
Bo góc 12–16px, đổ bóng nhẹ, icon nét mảnh đồng nhất.
Ưu tiên khả năng đọc bảng và biểu mẫu.
Tránh gradient lớn, hiệu ứng kính, hình minh họa chiếm quá nhiều diện tích.

Tạo khác biệt về bố cục:
- Sidebar nền xanh đậm, nhóm chức năng rõ ràng.
- Mục đang chọn có nền #2563EB, chữ và icon trắng, chỉ báo dễ nhận biết.
- Header có breadcrumb, tên người dùng, nhãn vai trò và menu tài khoản.
- Phần nội dung dùng tiêu đề lớn, mô tả ngắn và nút hành động chính.
- Trang chi tiết dùng bố cục hai cột: thông tin chính bên trái, trạng thái và hành động bên phải.
- Trang tài xế đơn giản hơn trang quản trị.
- Không thêm nút hoặc chỉ số trang trí không có chức năng.

Desktop 1440px là kích thước chính.
Có phiên bản mobile 390px cho các trang tài xế.
Mobile dùng menu thu gọn, biểu mẫu một cột và danh sách dạng card.

2. PHÂN QUYỀN VÀ ĐIỀU HƯỚNG

Menu QUẢN TRỊ VIÊN:
- Tổng quan
- Tài xế
- Phương tiện
- Phân công
- Phiên lái
- Vi phạm
- Thiết bị
- Loại xe
- Loại vi phạm
- Đổi mật khẩu
- Đăng xuất

Menu TÀI XẾ:
- Tổng quan
- Hồ sơ cá nhân
- Giấy phép lái xe
- Xe được giao
- Phiên lái của tôi
- Vi phạm của tôi
- Đổi mật khẩu
- Đăng xuất

Tài xế chỉ xem dữ liệu của chính mình.
Ẩn hoàn toàn chức năng quản trị khỏi menu tài xế.
Không có bộ chuyển vai trò trong ứng dụng thật.
Đăng nhập xác định vai trò từ tài khoản.
Đăng ký chỉ tạo tài khoản tài xế.

3. ĐĂNG NHẬP, ĐĂNG KÝ VÀ MẬT KHẨU

Trang đăng nhập:
- Logo VIA Fleet.
- Tên đăng nhập.
- Mật khẩu, nút hiện/ẩn mật khẩu.
- Nút Đăng nhập.
- Liên kết Đăng ký tài xế.
- Trạng thái sai thông tin đăng nhập.
- Đăng nhập thành công đến Tổng quan phù hợp vai trò.
- Không đưa tài xế đến trang quản lý tài xế của admin.
- Không thêm đăng nhập Google, OTP hoặc quên mật khẩu vì chưa có nghiệp vụ này.

Trang đăng ký:
- Tên đăng nhập.
- Email.
- Mật khẩu.
- Xác nhận mật khẩu.
- Đăng ký thành công tự đăng nhập và chuyển đến Hồ sơ cá nhân.
- Hiển thị thông báo yêu cầu bổ sung hồ sơ.

Trang đổi mật khẩu:
- Mật khẩu hiện tại.
- Mật khẩu mới.
- Nhập lại mật khẩu mới.
- Lỗi mật khẩu hiện tại không đúng hoặc xác nhận không khớp.
- Thành công giữ phiên đăng nhập hiện tại.

4. TỔNG QUAN QUẢN TRỊ

Hiển thị bốn chỉ số:
- Tổng phương tiện.
- Phiên đang lái.
- Phiên đã kết thúc.
- Hồ sơ chờ duyệt.

Bên dưới là bảng 10 phiên lái gần nhất:
- Mã phiên.
- Tài xế.
- Phương tiện.
- Thời gian bắt đầu.
- Thời gian kết thúc.
- Trạng thái.

Có liên kết đến danh sách phiên lái và hồ sơ chờ duyệt.
Không thêm bản đồ GPS, doanh thu, quãng đường hoặc biểu đồ dữ liệu chưa có.

5. QUẢN LÝ VÀ DUYỆT TÀI XẾ

Danh sách tài xế:
- Tìm theo họ tên, điện thoại, tên đăng nhập.
- Lọc trạng thái hồ sơ.
- Phân trang.
- Các cột: Họ tên, Điện thoại, Trạng thái hồ sơ, Trạng thái tài khoản.
- Nhấn một tài xế để mở trang chi tiết.
- Không có nút tạo tài xế thay cho luồng tự đăng ký.

Trạng thái hồ sơ:
- Thiếu thông tin.
- Chờ duyệt.
- Đã duyệt.
- Bị từ chối.

Trang chi tiết chia thành:
A. Thông tin cá nhân và trạng thái tài khoản.
B. Giấy phép lái xe và ảnh hai mặt.
C. Khuôn mặt và trạng thái duyệt.
D. Trạng thái hồ sơ tổng thể và các điều kiện còn thiếu.

Thông tin cá nhân:
- Họ tên, ngày sinh, số điện thoại, email, địa chỉ.
- Nút Vô hiệu hóa tài khoản hoặc Kích hoạt tài khoản.
- Có hộp thoại xác nhận khi vô hiệu hóa.

Duyệt GPLX:
- Xem số GPLX, hạng, ngày cấp, ngày hết hạn, ảnh trước và sau.
- GPLX chờ duyệt có nút Duyệt hoặc Từ chối.
- Không duyệt GPLX đã hết hạn.
- GPLX đã duyệt hoặc hết hạn có thể được yêu cầu làm lại.

Duyệt khuôn mặt:
- Xem ảnh đại diện.
- Hiển thị trạng thái đã có hoặc chưa có dữ liệu nhận diện.
- Có thể đặt dữ liệu vector chi tiết trong vùng mở rộng dành cho admin.
- Ảnh chờ duyệt có nút Duyệt hoặc Từ chối.
- Ảnh đã duyệt có thể được yêu cầu làm lại.
- Không cho duyệt khi chưa có dữ liệu nhận diện.

Duyệt hồ sơ tổng thể:
- Chỉ cho duyệt khi đủ thông tin, GPLX đã duyệt còn hạn, khuôn mặt đã duyệt.
- Hiển thị rõ điều kiện còn thiếu.
- Hồ sơ chờ duyệt có thể bị từ chối.
- Phân biệt trạng thái tài khoản với trạng thái hồ sơ.

6. HỒ SƠ CÁ NHÂN CỦA TÀI XẾ

Biểu mẫu:
- Họ và tên.
- Ngày sinh.
- Số điện thoại.
- Địa chỉ.
- Một ảnh đại diện/khuôn mặt.

Hiển thị trạng thái hồ sơ tổng thể và trạng thái ảnh khuôn mặt riêng.
Có danh sách những thông tin cần bổ sung.

Luồng:
- Chọn ảnh, xem trước, lưu hồ sơ.
- Thay ảnh tạo lại dữ liệu nhận diện và đưa ảnh về chờ duyệt.
- Không chọn ảnh mới thì giữ ảnh cũ.
- Thay thông tin quan trọng có thể yêu cầu duyệt lại.
- Đổi số điện thoại hoặc địa chỉ không mặc định yêu cầu duyệt lại.
- Thể hiện trạng thái đang xử lý và lỗi tải ảnh hoặc xử lý khuôn mặt.

Ảnh chấp nhận JPG, PNG, WebP, tối đa 5 MB và 20 megapixel.
Không có chức năng quay video, chụp nhiều góc mặt hoặc nhập vector thủ công.

7. GIẤY PHÉP LÁI XE CỦA TÀI XẾ

Biểu mẫu:
- Số GPLX.
- Hạng GPLX.
- Hệ hạng GPLX.
- Ngày cấp.
- Ngày hết hạn.
- Ảnh mặt trước.
- Ảnh mặt sau.

Hiển thị trạng thái:
- Chờ duyệt.
- Có hiệu lực.
- Hết hạn.
- Bị từ chối.

Lần đầu bắt buộc có đủ hai ảnh.
Lần cập nhật sau có thể thay riêng từng ảnh.
Sau khi cập nhật cần admin duyệt lại.
Ngày cấp không được ở tương lai.
Ngày hết hạn phải sau ngày cấp và sau ngày hiện tại.
Có trạng thái đang lưu, lỗi và lưu thành công.

8. PHƯƠNG TIỆN

Admin:
- Danh sách tìm kiếm, lọc trạng thái, phân trang.
- Các cột: Biển số, Loại xe, Hãng xe, Trạng thái.
- Có Thêm phương tiện và Chỉnh sửa.

Biểu mẫu:
- Biển số.
- Loại xe.
- Hãng xe.
- Mẫu xe.
- Năm sản xuất.
- Trạng thái.
- Mô tả.
- Với xe tải: trọng tải và khối lượng toàn bộ theo thiết kế.
- Với xe khách: số lượng hành khách và lựa chọn xe giường nằm.

Trạng thái:
- Hoạt động.
- Ngừng hoạt động.
- Đã thanh lý.

Không có thao tác xóa phương tiện.

Tài xế:
- Trang Xe được giao chỉ hiển thị xe có phân công đang hiệu lực.
- Chỉ xem, không thêm hoặc chỉnh sửa.
- Có trạng thái chưa được giao xe.

9. PHÂN CÔNG XE

Chỉ dành cho admin.

Danh sách:
- Tài xế.
- Phương tiện.
- Thời gian bắt đầu.
- Thời gian kết thúc.
- Tìm kiếm và phân trang.

Biểu mẫu:
- Chọn tài xế.
- Chọn phương tiện.
- Thời gian bắt đầu.
- Thời gian kết thúc không bắt buộc.

Điều kiện:
- Tài xế đang hoạt động, hồ sơ đầy đủ và đã duyệt.
- GPLX còn hạn và khuôn mặt đã duyệt.
- Xe đang hoạt động.
- Thời gian kết thúc phải sau thời gian bắt đầu.

Phân công đã có phiên lái:
- Không đổi tài xế, phương tiện hoặc thời gian bắt đầu.
- Chỉ cập nhật thời gian kết thúc phù hợp.

Phân công đang hiệu lực có nút “Kết thúc ngay” và hộp thoại xác nhận.
Phân công chưa bắt đầu hoặc đã kết thúc không có nút này.
Kết thúc phân công không tự kết thúc phiên lái đang diễn ra.
Không có thao tác xóa phân công.

10. PHIÊN LÁI

Admin xem tất cả; tài xế chỉ xem phiên của mình.

Bảng:
- Mã phiên.
- Tài xế.
- Xe.
- Bắt đầu.
- Kết thúc.
- Trạng thái Đang lái hoặc Đã kết thúc.

Có tìm kiếm, lọc trạng thái và phân trang.
Web chỉ xem dữ liệu phiên.
Việc mở và kết thúc phiên được thực hiện qua thiết bị trên xe.
Không tạo nút Bắt đầu lái hoặc Kết thúc phiên trên web.
Không tạo luồng sửa hoặc xóa phiên lái.

11. VI PHẠM VÀ DUYỆT VI PHẠM

Danh sách:
- Mã vi phạm.
- Tài xế.
- Xe.
- Loại vi phạm.
- Mức độ.
- Thời điểm phát hiện.
- Trạng thái.
- Tìm kiếm, lọc và phân trang.

Mức độ:
- Thấp.
- Trung bình.
- Cao.

Trạng thái:
- Chờ xác nhận.
- Đã xác nhận.
- Đã từ chối.
- Đã thu hồi.

Admin xem toàn bộ.
Tài xế chỉ xem vi phạm của chính mình ở trạng thái Chờ xác nhận hoặc Đã xác nhận.

Trang chi tiết:
- Thông tin tài xế, xe, phiên lái, thời điểm, loại, mức độ.
- Ghi chú của quản trị viên.
- Khu vực bằng chứng ảnh/video, thời gian ghi nhận, mở xem lớn.
- Trạng thái chưa có bằng chứng hoặc đường dẫn không hợp lệ.

Với admin và vi phạm chờ xác nhận:
- Được chỉnh loại vi phạm, mức độ và ghi chú.
- Có nút Xác nhận vi phạm và Từ chối.
- Có hộp thoại xác nhận.
- Chỉ xác nhận khi có bằng chứng hợp lệ.
- Không sửa tài xế, xe, phiên lái hoặc thời điểm phát hiện.

Với vi phạm đã xử lý:
- Có nút Xem xét lại để đưa về Chờ xác nhận nếu chưa có kháng cáo.
- Nếu đã có kháng cáo, hiển thị thông báo chức năng xử lý kháng cáo chưa được triển khai.

Admin có phần Lịch sử xử lý:
- Người xử lý.
- Thời gian.
- Quyết định.
- Loại vi phạm, mức độ, ghi chú sau xử lý.

Tài xế chỉ xem, không có nút duyệt và không thấy lịch sử xử lý nội bộ.
Không có nút tạo vi phạm thủ công.
Không tạo giao diện gửi hoặc xử lý kháng cáo trong phạm vi này.

12. THIẾT BỊ

Chỉ admin truy cập.

Danh sách:
- Mã thiết bị.
- Tên.
- Xe được gắn.
- Trạng thái.
- Kết nối gần nhất.

Trạng thái:
- Trực tuyến.
- Ngoại tuyến.
- Bảo trì.

Có thêm, sửa, tìm kiếm, lọc trạng thái và phân trang.
Biểu mẫu gồm mã, tên, xe và trạng thái.
Mỗi xe gắn tối đa một thiết bị.
Không chuyển thiết bị khỏi xe đang có phiên lái hoạt động.
Không thêm livestream, điều khiển camera, bản đồ hoặc tự cập nhật thời gian thực.

13. DANH MỤC

Loại xe:
- Danh sách và biểu mẫu tên, nhóm, mô tả.
- Nhóm Xe tải hoặc Xe khách.
- Thêm và sửa.
- Cho chọn nhiều loại xe để xóa.
- Chỉ xóa loại chưa được phương tiện sử dụng.
- Không đổi nhóm của loại đang được sử dụng.
- Hiển thị kết quả xóa thành công và các loại không thể xóa.

Loại vi phạm:
- Danh sách và biểu mẫu mã, tên, mô tả.
- Thêm và sửa.
- Ví dụ: DROWSINESS, PHONE_USAGE, DISTRACTION.
- Không thêm nút xóa.

14. TỔNG QUAN TÀI XẾ

Lời chào theo tên người dùng.
Ba chỉ số:
- Xe được giao.
- Phiên đang lái.
- Phiên đã kết thúc.

Bảng phiên lái gần đây chỉ của người đăng nhập.
Đặt các lối vào Hồ sơ cá nhân, GPLX, Xe được giao dễ tìm.
Không hiển thị số liệu toàn công ty hoặc danh sách tài xế khác.

15. TRẠNG THÁI VÀ TƯƠNG TÁC CHUNG

Thiết kế đầy đủ:
- Loading khi gửi biểu mẫu.
- Danh sách trống.
- Không có kết quả tìm kiếm.
- Lỗi ngay dưới trường nhập.
- Thông báo lưu thành công.
- Hộp thoại xác nhận thao tác quan trọng.
- Dữ liệu đã thay đổi ở nơi khác: yêu cầu tải lại trang trước khi lưu.
- Trang 403 thân thiện, giải thích không có quyền và nút Về tổng quan.
- Không dùng màu làm dấu hiệu duy nhất; luôn có nhãn trạng thái.

Các nút và liên kết trong prototype phải dẫn đến đúng màn hình hoặc trạng thái.
Giữ bảng màu, typography, khoảng cách, thành phần biểu mẫu nhất quán.

16. DỮ LIỆU MẪU

Dùng dữ liệu giả có tính nhất quán giữa các màn hình:
- Nguyễn Văn Minh, minh@example.com.
- Trần Quốc Huy, huy@example.com.
- Lê Hoàng Nam, nam@example.com.
- Xe tải Hyundai Mighty EX8, biển số 43C-218.65.
- Xe khách Thaco Town TB82S, biển số 43B-056.89.
- Xe tải Isuzu NQR, biển số 43C-192.34.
- Thiết bị RPI-001 và RPI-002.
- Loại vi phạm: Buồn ngủ, Sử dụng điện thoại, Mất tập trung.

Ngày tháng hiển thị dd/mm/yyyy.
Thời gian dùng định dạng 24 giờ.
Dùng cùng một tài xế, xe, mã phiên và mã vi phạm khi chuyển giữa danh sách và chi tiết.
Ảnh mẫu phải được hiểu là minh họa, không giả làm bằng chứng thật.

17. KẾT QUẢ MONG MUỐN

Tạo các màn hình thành một bộ thiết kế ứng dụng hoàn chỉnh, không phải landing page.

Ưu tiên trước:
1. Đăng nhập.
2. Tổng quan admin.
3. Danh sách tài xế.
4. Chi tiết và duyệt tài xế.
5. Danh sách vi phạm.
6. Chi tiết và duyệt vi phạm.
7. Tổng quan tài xế.
8. Hồ sơ cá nhân tài xế.

Sau đó tiếp tục các màn hình còn lại bằng cùng hệ thống thiết kế.
Đặt tên màn hình rõ vai trò, ví dụ:
“Admin / Tổng quan”
“Admin / Chi tiết tài xế”
“Tài xế / Hồ sơ cá nhân”.

Mục tiêu là thay đổi nhận diện và cách trình bày, đồng thời giữ nguyên quyền truy cập, dữ liệu và luồng nghiệp vụ đã mô tả.
