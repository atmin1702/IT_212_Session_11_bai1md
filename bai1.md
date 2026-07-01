# Bài 1: Phân Tích & Lựa Chọn Phương Án Tạo Mã Nguồn (Lesson 01)

## Đáp án được chọn: Phương án B

---

## Phân tích lý do chọn Phương án B

Phương án B là phương án tối ưu nhất vì đã áp dụng **đầy đủ cấu trúc 5 thành phần** của một Prompt chuyên nghiệp:

- **Vai trò (Role):** *"Đóng vai Senior Java Developer"*
  - Giúp AI định hình phong cách lập trình chuyên nghiệp, viết code chuẩn enterprise thay vì code demo đơn giản.
  - AI sẽ ưu tiên các best practices như đặt tên biến rõ ràng, xử lý ngoại lệ đúng cách.

- **Nhiệm vụ / Mục tiêu (Task/Goal):** *"Viết class PaymentValidator kiểm tra tính hợp lệ của thẻ tín dụng"*
  - Xác định rõ ràng, cụ thể tên class (`PaymentValidator`) và chức năng duy nhất cần thực hiện.
  - AI không bị phân tán sang các tác vụ không liên quan.

- **Ngữ cảnh (Context):** *"Hệ thống E-commerce, cần validate trước khi gửi API thanh toán"*
  - Giúp AI hiểu rõ môi trường triển khai (hệ thống thương mại điện tử).
  - AI biết đây là bước tiền xử lý (pre-processing) trước khi gọi API, từ đó thiết kế class phù hợp (chỉ validate, không xử lý thanh toán).

- **Ràng buộc (Constraints):** *"Dùng Java 17, triển khai thuật toán Luhn, ném IllegalArgumentException nếu thẻ rỗng hoặc chứa chữ cái"*
  - Ép AI sử dụng đúng phiên bản Java yêu cầu (Java 17).
  - Chỉ định rõ thuật toán phải dùng (Luhn) — tránh AI tự chọn thuật toán khác.
  - Xác định rõ loại Exception cần ném (`IllegalArgumentException`) và điều kiện kích hoạt — đảm bảo xử lý ngoại lệ khớp với chuẩn dự án.

- **Định dạng (Format):** *"Chỉ trả về mã nguồn Java trong một code block, không giải thích"*
  - Đầu ra gọn gàng, dễ dàng copy/paste trực tiếp vào IDE mà không cần lọc bỏ phần text giải thích.
  - Tiết kiệm thời gian cho developer.

---

## Phân tích lỗ hổng của các phương án bị loại trừ

### Phương án A
*Prompt: "Viết cho tôi một class Java tên là PaymentValidator để kiểm tra số thẻ tín dụng bằng thuật toán Luhn. Code ngắn gọn thôi nhé."*

- **Thiếu Vai trò (Role):** Không gán vai trò cho AI → AI có thể sinh code ở mức sinh viên thay vì mức chuyên nghiệp.
- **Thiếu Ngữ cảnh (Context):** Không đề cập đây là hệ thống E-commerce hay bất kỳ môi trường nào → AI không có cơ sở để đưa ra quyết định thiết kế phù hợp.
- **Thiếu Ràng buộc (Constraints):** Không chỉ định phiên bản Java, không yêu cầu xử lý ngoại lệ cụ thể → AI có thể dùng Java 8, bỏ qua việc validate input rỗng hoặc chứa ký tự không hợp lệ.
- **Thiếu Định dạng (Format):** Không giới hạn output → AI có thể sinh kèm đoạn văn giải thích dài dòng, lẫn lộn với code.
- **Rủi ro:** Cụm từ "Code ngắn gọn thôi nhé" mang tính cảm tính, có thể khiến AI cắt bớt phần xử lý edge case quan trọng (như kiểm tra null, chuỗi rỗng) để cho "ngắn gọn".

### Phương án C
*Prompt: "Tôi cần một đoạn code kiểm tra thẻ tín dụng. Hãy viết bằng Java và sinh thêm cả database SQL để lưu thông tin thẻ. Nhớ hướng dẫn tôi cách cài đặt database và kết nối JDBC luôn nhé."*

- **Thiếu Vai trò (Role):** Không gán vai trò → AI không có định hướng chuyên môn cụ thể.
- **Sai lệch Ngữ cảnh (Context Drift):** Yêu cầu ôm đồm quá nhiều tác vụ không liên quan (tạo database SQL, hướng dẫn cài đặt, kết nối JDBC) trong khi nhiệm vụ chính chỉ là validate số thẻ tín dụng.
- **Thiếu Ràng buộc (Constraints):** Không chỉ định thuật toán Luhn, không yêu cầu xử lý ngoại lệ, không giới hạn phiên bản Java.
- **Rủi ro ảo tưởng (Hallucination):**
  - AI có thể tự bịa ra cấu trúc bảng SQL không tồn tại trong hệ thống thực tế.
  - Hướng dẫn cài đặt database có thể không khớp với hạ tầng kỹ thuật của dự án (ví dụ hướng dẫn MySQL trong khi dự án dùng PostgreSQL).
  - Phần code JDBC kết nối có thể chứa thông tin cấu hình sai (host, port, credentials) mà developer mới vào dự án có thể dùng nhầm.
- **Vi phạm nguyên tắc Separation of Concerns:** Validation logic và Database logic nên nằm ở các tầng (layer) khác nhau trong kiến trúc phần mềm. Prompt này khiến AI trộn lẫn hai trách nhiệm vào cùng một chỗ.
