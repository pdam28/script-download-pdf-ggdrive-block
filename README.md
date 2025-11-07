Script Tải Ảnh (Blob) sang PDF
Đây là một đoạn mã JavaScript mạnh mẽ được thiết kế để chạy trong trình duyệt (dưới dạng Bookmarklet hoặc qua Console). Nó tự động quét, cuộn và tải xuống tất cả các hình ảnh có nguồn blob: trên một trang web và tổng hợp chúng thành một file PDF duy nhất.

🌟 Tính năng chính
Tự động cuộn thông minh: Tự động cuộn trang chính VÀ tất cả các khung cuộn con bên trong để kích hoạt "lazy loading", đảm bảo thu thập đủ 100% ảnh.

Tổng hợp PDF: Sử dụng thư viện jsPDF (tải tự động) để ghép tất cả ảnh tìm được thành một file PDF duy nhất.

Chất lượng cao: Giữ nguyên độ phân giải gốc của ảnh (dùng naturalWidth/naturalHeight) và tự động tính toán tỉ lệ px sang pt (0.75) để PDF có kích thước chính xác.

Thông báo trạng thái: Hiển thị một hộp thông báo trực quan ở góc trên bên phải màn hình để người dùng biết chính xác điều gì đang xảy ra (ví dụ: "Đang cuộn...", "Đang xử lý ảnh 5/150...").

Tương thích bảo mật: Hoạt động trên các trang web hiện đại có Chính sách Bảo mật Nội dung (CSP) nghiêm ngặt, bao gồm cả xử lý TrustedTypes cho script.src và TrustedHTML (textContent).

🚀 Cách sử dụng (Dành cho khách hàng)
Cách dễ nhất, an toàn nhất và được khuyên dùng là cài đặt script này dưới dạng Bookmarklet (Dấu trang).

Cài đặt một lần
Mở file HTML: Mở file taipdf.html (file HTML bạn nhận được) trong trình duyệt của bạn.

Hiển thị Thanh Dấu trang: Nếu thanh Dấu trang (Bookmark Bar) bị ẩn, hãy nhấn Ctrl + Shift + B (Windows) hoặc Cmd + Shift + B (Mac) để nó hiện ra.

Kéo và Thả: Nhấn giữ chuột vào nút màu xanh "KÉO & THẢ ĐỂ TẢI PDF" và kéo nó lên Thanh Dấu trang của bạn, sau đó thả ra.

Bạn sẽ thấy một bookmark mới xuất hiện. Bạn có thể nhấp chuột phải vào nó để "Chỉnh sửa" (Edit) và đổi tên thành tên gì đó ngắn gọn (ví dụ: Tải PDF).

Sử dụng hàng ngày
Mở trang web có chứa các ảnh blob: mà bạn muốn tải.

Nhấp vào bookmark Tải PDF mà bạn vừa lưu trên thanh.

Script sẽ tự động chạy. Hộp thông báo sẽ hiện ở góc trên bên phải.

Khi hoàn tất, file PDF sẽ được tự động tải về máy.

👨‍💻 Cách sử dụng (Dành cho Lập trình viên / Nâng cao)
Bạn cũng có thể chạy script trực tiếp từ Console của trình duyệt.

Mở trang web bạn muốn tải ảnh.

Nhấn F12 (hoặc Ctrl+Shift+I / Cmd+Opt+I) để mở Developer Tools.

Chuyển sang tab Console.

Sao chép (copy) toàn bộ nội dung của file script JavaScript (phiên bản "siêu tự động cuộn").

Dán (paste) nó vào Console và nhấn Enter.

Script sẽ thực hiện các bước tương tự như Bookmarklet.

⚠️ Hạn chế / Lưu ý
Chỉ tải ảnh blob:: Script này được thiết kế đặc biệt để chỉ tìm các ảnh có src bắt đầu bằng blob:. Nó sẽ không tải các ảnh .jpg, .png hay base64 thông thường.

Giới hạn bộ nhớ: Với các trang cực kỳ nặng (ví dụ: 1000+ ảnh chất lượng cao), script có thể chạy chậm hoặc làm trình duyệt bị treo do giới hạn bộ nhớ RAM của một tab. (Phiên bản script này không chia nhỏ file PDF).

Cấu trúc trang phức tạp: Mặc dù script đã cố gắng cuộn tất cả các phần tử, một số trang web có cấu trúc quá phức tạp hoặc dùng kỹ thuật ảo hóa (virtualization) có thể cản trở việc thu thập ảnh.
