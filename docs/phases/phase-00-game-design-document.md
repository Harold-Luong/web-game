# Phase 00 — Game Design Document

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | A — Thiết kế trước khi code |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Thiết kế bằng tài liệu |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Chốt concept, core loop, phạm vi MVP, nền tảng, cách thắng/thua và điểm còn mở.

## Đầu vào và phụ thuộc

- Không phụ thuộc phase triển khai; cần yêu cầu sản phẩm trong README và thông tin người dùng đã cung cấp.

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Chốt nền tảng, góc nhìn, cách điều khiển và quy tắc đội hình trước khi triển khai client.

## Các bước thực hiện

1. Xác định nền tảng, góc nhìn, input và vòng chơi; phân biệt sản phẩm co-op với prototype Warrior solo.
2. Mô tả đội hình, chọn class, bắt đầu dungeon, thắng/thua, chết/revive và chơi lại.
3. Chia MVP và phần ngoài MVP; ghi quyết định đã chốt, giả thuyết và câu hỏi cần người dùng quyết định.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `docs/design/GDD.md`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Code, scaffold, asset, công thức combat chi tiết và thiết kế hạ tầng.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ viết tài liệu thiết kế. Đánh dấu đề xuất và quyết định còn mở; không coi đặc tả giao việc này là đầu ra thiết kế đã hoàn thành.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] GDD có luồng từ vào game đến kết quả, gồm cả đường thất bại.
- [ ] Đủ 4 vai trò và mục tiêu teamwork; không tự đổi thành sản phẩm solo.
- [ ] Có phạm vi riêng cho vertical slice, dungeon offline và multiplayer MVP.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Đọc thử một lượt thắng, một lượt team wipe và một trường hợp thiếu class theo GDD; mỗi bước phải có kết quả hoặc câu hỏi còn mở được chỉ rõ.

Kiểm tra liên kết, thuật ngữ và sự nhất quán với README/các đặc tả liên quan. Không tạo code hoặc dependency chỉ để kiểm tra tài liệu.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-00-game-design-document.md. Thực hiện chỉ Phase 0 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 0, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

