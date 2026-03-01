# Báo Cáo Dự Án: Website Tích Hợp AI Trợ Lý "VanAnh Writes"

Xin chào các thành viên nhóm! Trọng tâm của tài liệu này là giúp các bạn nắm rõ kiến trúc, những công nghệ đang được sử dụng và luồng hoạt động của Website AI Chatbot mà nhóm chúng ta xây dựng.

Tài liệu này sẽ cực kỳ có ích khi các bạn làm Slide thuyết trình hoặc viết Báo cáo môn học.

---

## 1. Công Nghệ Được Sử Dụng

Toản bộ dự án được thiết kế **"Frontend Only"** (Không cần cài đặt Database hay Backend Node.js phức tạp) nhằm tạo sự nhẹ nhàng, dễ chạy báo cáo ở bất kỳ máy tính nào bằng cách mở thẳng file HTML.

*   **HTML5 (Cấu trúc):** Dùng để lên khung xương toàn bộ Landing Page và cấu trúc của tiện ích (Widget) Chatbot AI nổi ở góc phải.
*   **Tailwind CSS (via CDN):** Framework thiết kế giao diện dạng Utility-first. Nhóm lựa chọn cách chạy thẳng qua CDN (`<script src="https://cdn.tailwindcss.com"></script>`) để không phải biên dịch (Build), phù hợp cho dự án cần chạy tức thì. Giao diện được lấy cảm hứng từ các nền tảng AI hiện đại (Linear, OpenAI) với tông màu Tím / Xanh / Slate Dark.
*   **Vanilla JavaScript (JS thuần - Logic):** Là "Bộ Não" của Frontend. Dùng để xử lý các hành vi nhấp chuột (onClick), ẩn/hiện popup chat (toggle), và **vô cùng quan trọng** là xử lý hàm Fetch API giao tiếp với Google.
*   **Google Gemini API (AI Intelligence):** Đây là lõi xử lý AI thật sự. Thay vì xây dựng 1 Model ngôn ngữ riêng (rất tốn kém), nhóm sử dụng hàm gọi REST qua API `v1beta` đến mô hình **`gemini-2.5-flash`** (mô hình AI tân tiến nhất của Google ở thời điểm đó dành cho sinh viên/tài khoản miễn phí).
*   **FontAwesome (Qua CDN):** Để hiển thị toàn bộ icon đẹp mắt trên website (Icon Robot, Nút gửi, Nút phóng to thu nhỏ).
*   **Vercel (Hosting/Deployment):** Nền tảng chuyên dụng dùng để Deploy Code từ tài khoản Github của mình (`Longanh0168`) thành 1 trang Web chạy thật trên đường Link `.vercel.app`.

---

## 2. Cách Thức Tạo Khung Website Bề Mặt

*   Cấu trúc của trang là **Landing Page (Trang đích dạng cuộn 1 trang)**. Bao gồm 1 Navbar cố định trên cùng (`fixed z-50`), một phần `Hero Section` đập vào mắt người xem bằng gradient sống động, danh sách tính năng `Features Section`, và phần giới thiệu luồng sử dụng `How It Works`.
*   Tất cả sử dụng hệ thống Lưới (`grid-cols-1 md:grid-cols-2`) và linh hoạt hình (`flex`) của Tailwind CSS để đảm bảo: Trang có thể tự thu gọn thành hàng dọc nếu người dùng xem trên điện thoại, và dàn ngang cực đẹp nếu xem trên Màn hình máy tính (Responsive Design).
*   Tại `Hero Section`, bên phải có Mockup bộ ảnh 1 đoạn Chat tĩnh nhằm Minh hoạ cho chức năng, chứ không phản hồi vì nó chỉ là ảnh Decor trực quan.

---

## 3. Bí Mật Bên Trong Chatbot "VanAnh Writes AI"

Đây là giá trị lõi cao nhất của bài tập, cần phải xoáy sâu vào khi báo cáo / phản biện giáo viên:

### a) Widget lơ lửng và Phóng To
Toàn bộ Chatbot là một khối thẻ tĩnh (nằm ở `id="ai-chat-window"`), được thiết lập `fixed bottom-20 right-0`. Bằng Javascript, nút bật tắt sẽ thêm/xoá class `hidden` của Tailwind để tạo hiệu ứng tắt/bật Chatbot. Nút "Expand (Phóng to)" thực hiện đổi class biến nó thành `fixed inset-0` - lấp đầy 100% màn hình dành cho trải nghiệm Full-screen.

### b) Cơ chế Hai Chế Độ (Fallback & AI Thật)
Để phòng ngừa sự cố mạng hoặc bạn bị chấm điểm khi... hết dung lượng API Key:
*   Mặc định, khi vừa mở web, thẻ Chatbot có sẵn lệnh nhắc người dùng **Dán Google Gemini API Key** vào ô. Code sẽ dùng `localStorage.setItem('gemini_api_key', key)` để "Nhớ" nó vô trình duyệt (để F5 không bị mất). Mật khẩu này CHỈ được dùng ở chính máy của người mở web, không bao giờ gửi đi đâu ngoại trừ Google, rất bảo mật.
*   **Chế độ Offline Simulator:** Nếu bạn KHÔNG nhập Key vào, bạn cứ chat, Bot vẫn tự động hồi đáp. Đây là hàm Fallback (Chống treo dự án). Nó sẽ bắt các Keywords có sẵn ("Viết cho tôi", "Chào") và in ra trước 1 một số Template văn bản mồi ảo để "Chữa cháy lúc lên báo cáo mà mất mạng".

### c) Kỹ thuật Gửi Request và Context Nhận diện (Quan Trọng!)
Nếu có API Key hợp lệ, vòng đời tin nhắn diễn ra như sau:
1.  **Thu thập yêu cầu:** Khi nhấn Enter, JS lấy kí tự từ thẻ input.
2.  **Prompt Engineering (Kỹ nghệ mồi):** Đây là kỹ thuật ăn điểm. Trước khi gửi cho Gemini, JS gọi `new Date().toLocaleString('vi-VN')` để gắp Thời Gian Hiện Khắc của Hệ thống máy tính. Sau đó tạo ra 1 `systemPrompt` (Câu lệnh hệ thống vô hình đối với màn hình User):
    *   *Tôi tiêm (inject) vào não AI rằng: Ngươi tên là Vân Anh, phục vụ cho VanAnh Writes, ngôn ngữ là tiếng Việt chân thực, ngày giờ hiện tại là ABC... và sau đó mới nối thêm Câu hỏi của Người dùng vào cuối cùng.*
3.  **Fetch Connect:** Dùng `await fetch` theo phương thức POST (chứ không phải GET) gửi chuỗi System Prompt kia cùng với API Key kèm vào đuôi URL qua mạng lên Server Google (model `gemini-2.5-flash`).
4.  **Parsing & Output:** Gemini nhả luồng văn bản (JSON) xuống. JS sẽ đi gỡ `response.json()`, chui tới đường dẫn kết quả mảng cuối cùng (`data.candidates[0].content.parts[0].text`), lấy nó và in chuỗi HTML thẻ `<div class='... text-gray-700 bg-white...'>` đính thẳng vào Giao diện khung Chat cho người xem. Lặp tức, cuộn trình duyệt của khung chat sẽ tự giật xuống cuối (`msgs.scrollTop = msgs.scrollHeight`).

---
_Hy vọng tài liệu này sẽ giúp nhóm ăn trọn điểm 10 trong buổi báo cáo sắp tới!_
