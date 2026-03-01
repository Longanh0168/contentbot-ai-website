# Website + AI Integration Plan

## Goal
Tạo website Landing Page giới thiệu sản phẩm nhóm và tích hợp AI Chatbot hoạt động thực tế, hỗ trợ báo cáo chi tiết các bước.

## Tóm tắt Ý tưởng & Công nghệ
- **Mô hình Website**: Landing Page (Trang đơn cuốn chiếu) gồm đầy đủ các mục: Giới thiệu chung, Tính năng nổi bật, Hướng dẫn sử dụng.
- **Công nghệ Frontend**: Nên sử dụng Vite + React + TailwindCSS (hoặc chỉ HTML/Tailwind) để giao diện hiện đại, mượt mà và dễ responsive.
- **Công nghệ AI Chatbot**: Thay vì code AI từ đầu tốn kém, tôi đề xuất dùng **Google Gemini**, **Chatbase** hoặc **Dialogflow**. Ta sẽ tạo một agent trên đó, cấp dữ liệu về sản phẩm, sau đó lấy đoạn mã nhúng (Embed Script/Iframe) dán vào web. Khung chat sẽ hiển thị dạng bong bóng (Floating Widget) ở góc phải dưới màn hình.
- **Triển khai (Hosting)**: Vercel hoặc Netlify (miễn phí, nhanh, có chứng chỉ bảo mật HTTPS, uy tín khi gửi link cho giảng viên).
- **Tạo Mã QR**: Dùng thư viện mã nguồn mở hoặc web tạo QR miễn phí trỏ về link Vercel.

## Tasks
- [ ] Task 1: Khởi tạo cấu trúc dự án và thiết lập màu sắc/UI tổng thể → Verify: Dự án chạy cục bộ thành công.
- [ ] Task 2: Xây dựng Section "Giới thiệu sản phẩm" (Hero Section) → Verify: Có tiêu đề lớn, hình/video minh hoạ, nút kêu gọi hành động.
- [ ] Task 3: Xây dựng Section "Tính năng" và "Hướng dẫn" → Verify: Hiển thị mạch lạc bằng các thẻ Grid/Card, rõ ràng từng bước sử dụng phần mềm/bài tập nhóm.
- [ ] Task 4: Cấu hình và nhúng AI Chatbot → Verify: Dán script nhúng thành công, bong bóng chat xuất hiện trên web và chat nhận được phản hồi.
- [ ] Task 5: Tối ưu hoá Mobile Responsive → Verify: Giao diện không vỡ, nút chat không che khuất chữ khi mở bằng điện thoại.
- [ ] Task 6: Deploy lên Vercel để lấy link chính thức và tạo ảnh QR → Verify: Link dạng `tensanpham.vercel.app` hoạt động, cấp quyền public.
- [ ] Task 7: Hỗ trợ tạo dữ liệu chụp hình báo cáo (step-by-step cho Báo cáo Nhiệm vụ 2) → Verify: Hoàn tất tài liệu minh chứng.

## Done When
- [ ] Website hiển thị đẹp, tối ưu UX/UI trên cả Desktop và Smartphone.
- [ ] Chatbot hoạt động ổn định trực tiếp ngay trên web (không cần link ngoài).
- [ ] Link Website thực tế kiểm tra được bởi Giảng viên.
