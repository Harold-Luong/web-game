# Phase 09 — Hitbox/hurtbox

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | B — Vertical slice một người chơi |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Hit được xác định bởi va chạm và thời điểm có hiệu lực.

## Đầu vào và phụ thuộc

- [Phase 08 — Skill system](phase-08-skill-system.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Hit là kết quả hình học/thời gian; HP sẽ do Phase 10 xử lý qua pipeline.

## Các bước thực hiện

1. Định nghĩa vùng gây hit và vùng nhận hit riêng; chuyển hình học theo vị trí/hướng.
2. Kích hoạt hitbox theo cửa sổ skill; thu kết quả giao nhau theo ID mục tiêu.
3. Theo dõi mục tiêu đã trúng trong một cast; hỗ trợ quy tắc multi-hit đã chốt và dọn hitbox khi hủy/chết.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/combat/`; `tích hợp skill và entity`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Công thức damage đầy đủ, loot và physics nâng cao không phục vụ MVP.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ client offline và Warrior prototype. Tái dùng các phần đã có; chưa thêm backend, tài khoản, persistence hoặc networking.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Mục tiêu ngoài vùng hoặc ngoài thời gian hiệu lực không bị nhận hit.
- [ ] Một đòn single-hit không tạo nhiều hit chỉ vì hai vùng chạm nhau nhiều frame.
- [ ] Quay hướng, di chuyển và hủy cast không để hitbox sai vị trí hoặc tồn tại vĩnh viễn.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Thử dummy ở trong/ngoài/rìa vùng, giữ giao nhau nhiều tick và hủy đòn; kiểm tra hình học với dữ liệu cố định.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-09-hitbox-hurtbox.md. Thực hiện chỉ Phase 9 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 9, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

