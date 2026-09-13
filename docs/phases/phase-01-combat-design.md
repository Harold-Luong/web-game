# Phase 01 — Combat design

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | A — Thiết kế trước khi code |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Thiết kế bằng tài liệu |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Stat, công thức damage, trạng thái, hit timing và quy tắc cooldown đủ rõ để triển khai.

## Đầu vào và phụ thuộc

- [Phase 00 — Game Design Document](phase-00-game-design-document.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Các hằng số ban đầu là đề xuất có nhãn; chốt minimum damage, tài nguyên và friendly fire trước Phase 8–10.

## Các bước thực hiện

1. Định nghĩa stat, đơn vị, miền giá trị, công thức damage và quy tắc làm tròn/clamp.
2. Lập bảng trạng thái, tác động lên di chuyển/thi triển, ưu tiên và cách kết hợp shield, stun, slow, invulnerable, dead.
3. Mô tả vòng đời đòn đánh, thời gian hiệu lực hitbox, cooldown, multi-hit, targeting và tài nguyên nếu có.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `docs/design/COMBAT.md`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Triển khai damage system, cân bằng toàn game hoặc thêm hệ nguyên tố phức tạp.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ viết tài liệu thiết kế. Đánh dấu đề xuất và quyết định còn mở; không coi đặc tả giao việc này là đầu ra thiết kế đã hoàn thành.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Có ví dụ số cho đòn thường, defense cao, shield và mục tiêu đã chết.
- [ ] Một lần cast có quy tắc hit lại và cooldown không mơ hồ.
- [ ] Phân biệt logic combat với animation; quy tắc có thể dùng cho client offline và server sau này.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Tính tay các ví dụ biên và lần theo một cast bị ngắt; kiểm tra cùng input không dẫn đến hai cách hiểu khác nhau.

Kiểm tra liên kết, thuật ngữ và sự nhất quán với README/các đặc tả liên quan. Không tạo code hoặc dependency chỉ để kiểm tra tài liệu.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-01-combat-design.md. Thực hiện chỉ Phase 1 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 1, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

