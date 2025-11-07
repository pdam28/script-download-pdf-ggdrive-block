# Script Tải Ảnh (Blob) sang PDF

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![jsPDF](https://img.shields.io/badge/jsPDF-FF0000?style=for-the-badge&logo=adobeacrobatreader&logoColor=white)

Đây là một đoạn mã JavaScript mạnh mẽ được thiết kế để chạy trong trình duyệt (dưới dạng **Bookmarklet** hoặc qua **Console**). Nó tự động quét, cuộn và tải xuống tất cả các hình ảnh có nguồn `blob:` trên một trang web và tổng hợp chúng thành một file PDF duy nhất.

---

## 🌟 Tính năng chính

* **Tự động cuộn thông minh**: Tự động cuộn trang chính VÀ **tất cả các khung cuộn con** bên trong để kích hoạt "lazy loading", đảm bảo thu thập đủ 100% ảnh.
* **Tổng hợp PDF**: Sử dụng thư viện `jsPDF` (tải tự động) để ghép tất cả ảnh tìm được thành một file PDF duy nhất.
* **Chất lượng cao**: Giữ nguyên độ phân giải gốc của ảnh (dùng `naturalWidth`/`naturalHeight`) và tự động tính toán tỉ lệ `px` sang `pt` (0.75) để PDF có kích thước chính xác.
* **Thông báo trạng thái**: Hiển thị một hộp thông báo trực quan ở góc trên bên phải màn hình để người dùng biết chính xác điều gì đang xảy ra (ví dụ: "Đang cuộn...", "Đang xử lý ảnh 5/150...").
* **Tương thích bảo mật**: Hoạt động trên các trang web hiện đại có Chính sách Bảo mật Nội dung (CSP) nghiêm ngặt, bao gồm cả xử lý `TrustedTypes` cho `script.src` và `TrustedHTML` (`textContent`).

---

## 🚀 Cách sử dụng (Cho người dùng)

Cách dễ nhất, an toàn nhất và được khuyên dùng là cài đặt script này dưới dạng **Bookmarklet** (Dấu trang).

### Cài đặt một lần

1.  **Mở file HTML**: Mở file `taipdf.html` (file HTML đi kèm) trong trình duyệt của bạn.
2.  **Hiển thị Thanh Dấu trang**: Nếu thanh Dấu trang (Bookmark Bar) bị ẩn, hãy nhấn `Ctrl + Shift + B` (Windows) hoặc `Cmd + Shift + B` (Mac) để nó hiện ra.
3.  **Kéo và Thả**: Nhấn giữ chuột vào nút màu xanh **"KÉO & THẢ ĐỂ TẢI PDF"** và kéo nó lên Thanh Dấu trang của bạn, sau đó thả ra.
4.  Bạn sẽ thấy một bookmark mới xuất hiện. (Bạn có thể nhấp chuột phải vào nó để "Chỉnh sửa" và đổi tên thành `Tải PDF` cho gọn).

### Sử dụng hàng ngày

1.  Mở trang web có chứa các ảnh `blob:` mà bạn muốn tải.
2.  Nhấp vào bookmark `Tải PDF` mà bạn vừa lưu trên thanh.
3.  Script sẽ tự động chạy, cuộn trang để tải tất cả ảnh.
4.  Khi hoàn tất, file PDF sẽ được tự động tải về máy.

---

## 👨‍💻 Mã nguồn (Source Code)

Bạn có thể xem toàn bộ mã nguồn, đã được format và bình luận đầy đủ, tại file:

### ➡️ [code.js](./code.js) ⬅️
*(Giả sử file của bạn tên là `code.js` và nằm cùng thư mục)*

---

### 🔬 Xem nhanh (Code Preview)

⚠️ **Lưu ý:** Đây chỉ là một **đoạn trích** (snippet) để xem nhanh logic cuộn tự động. Toàn bộ code nằm trong file [code.js](./code.js).

```javascript
    // --- 3. HÀM SIÊU TỰ ĐỘNG CUỘN (async/await) ---
    async function superAutoScroll() {
        console.log("Bắt đầu cuộn trang chính (window)...");
        statusDiv.textContent = "Đang cuộn trang chính...";
        
        // BƯỚC 1: Cuộn trang chính (window) xuống dưới cùng
        await new Promise(resolve => {
            let totalHeight = 0;
            let distance = 200; // Cuộn 200px mỗi lần
            let timer = setInterval(() => {
                // ... logic cuộn ...
                if (/* đã cuộn hết */) {
                    clearInterval(timer);
                    resolve(); // Báo là xong bước 1
                }
            }, 100); 
        });
        
        console.log("Đã cuộn xong trang chính. Tìm kiếm khung cuộn bên trong...");
        statusDiv.textContent = "Đang tìm khung cuộn bên trong...";

        // BƯỚC 2: Tìm TẤT CẢ các element khác có thanh cuộn
        const scrollableElements = [];
        document.querySelectorAll('*').forEach(el => {
            if (el.scrollHeight > el.clientHeight && (/*...có style cuộn...*/)) {
                scrollableElements.push(el);
            }
        });

        // BƯỚC 3: Cuộn lần lượt TỪNG element tìm được
        for (const [index, el] of scrollableElements.entries()) {
            statusDiv.textContent = `Đang cuộn khung phụ ${index + 1}/${scrollableElements.length}...`;
            await new Promise(resolve => {
                 // ... logic cuộn element con ...
                let timer = setInterval(() => {
                    if (/* đã cuộn hết element này */) {
                        clearInterval(timer);
                        resolve(); // Báo là xong element này
                    }
                }, 100);
            });
        }

        // BƯỚC 4: Tất cả đã được cuộn! Bắt đầu tạo PDF
        console.log("Đã cuộn tất cả. Chờ 2 giây cho ảnh tải.");
        statusDiv.textContent = "Đã cuộn xong. Chờ 2s cho ảnh tải...";
        setTimeout(startPdfGeneration, 2000); // Chờ 2 giây cuối cùng
    }
