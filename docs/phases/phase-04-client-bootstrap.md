# Phase 04 — Client bootstrap

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | B — Vertical slice một người chơi |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Client TypeScript/Vite/Phaser mở được trong browser với BootScene và GameScene.

## Đầu vào và phụ thuộc

- [Phase 00 — Game Design Document](phase-00-game-design-document.md).
- [Phase 01 — Combat design](phase-01-combat-design.md).
- [Phase 02 — Class design](phase-02-class-design.md).
- [Phase 03 — Boss mechanic design](phase-03-boss-mechanic-design.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Cần đầu ra thiết kế Phase 0–3 đủ để chọn góc nhìn/input; không tự coi file giao việc thiết kế là GDD đã hoàn thành.

## Các bước thực hiện

1. Kiểm tra môi trường và chọn phiên bản TypeScript/Vite/Phaser tương thích; ghi package manager và phiên bản.
2. Khởi tạo client tối thiểu, BootScene tải dữ liệu cần thiết và GameScene hiển thị map/player placeholder.
3. Bổ sung lệnh phát triển, build và typecheck phù hợp; ghi cách khởi động và cấu trúc thư mục thực sự có.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/`; `README.md — hướng dẫn chạy thực tế`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Movement, combat, enemy, login và backend.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ client offline và Warrior prototype. Tái dùng các phần đã có; chưa thêm backend, tài khoản, persistence hoặc networking.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Mở client thấy map và một placeholder với kích thước/điểm neo rõ ràng.
- [ ] Build và kiểm tra TypeScript chạy thành công bằng lệnh có thật.
- [ ] Không có Spring Boot, DB, network hoặc gameplay ngoài bootstrap.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chạy lệnh cài/build/typecheck đã khai báo; mở browser kiểm tra canvas, resize cơ bản và console. Nếu không có browser, báo phần chưa xác minh.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-04-client-bootstrap.md. Thực hiện chỉ Phase 4 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 4, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

