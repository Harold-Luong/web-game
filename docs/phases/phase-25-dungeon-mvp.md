# Phase 25 — Dungeon MVP

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | D — Dungeon hoàn chỉnh |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Một dungeon tĩnh chạy từ đầu đến kết quả, có phòng thường, mini boss và boss.

## Đầu vào và phụ thuộc

- [Phase 21 — Dungeon architecture](phase-21-dungeon-architecture.md).
- [Phase 22 — Enemy variety](phase-22-enemy-variety.md).
- [Phase 23 — Mini boss](phase-23-mini-boss.md).
- [Phase 24 — Full Golem](phase-24-full-golem.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** M4 cần review gameplay trước network; ghi phần đánh giá của người chơi còn thiếu nếu chưa có phản hồi.

## Các bước thực hiện

1. Ghép start room, combat rooms, mini boss, rest room, Golem và màn hình kết quả.
2. Tuning sơ bộ số wave/quái và thời lượng theo giả thuyết được ghi, kiểm tra pacing bốn class.
3. Hoàn thiện restart, reset trạng thái giữa lượt và tài liệu chơi thử/gate M4.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/dungeon/`; `scene vòng chơi và cấu hình dungeon đầu`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Spring Boot, WebSocket, login, DB, inventory, Redis hoặc dungeon thứ hai.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Một dungeon tĩnh offline. Giữ các quy tắc class/boss đã thiết kế; chưa thêm Spring Boot, DB hoặc Redis.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Chơi được dungeon từ đầu đến thắng/thua với bốn class trong mô phỏng offline.
- [ ] Các cửa, wave và encounter không chặn tiến trình sau khi đã đạt điều kiện.
- [ ] Có ghi nhận thời lượng, độ rõ mechanic và vấn đề của từng vai trò từ lượt chơi thật.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chơi trọn lượt thắng, wipe ở mini boss/Golem rồi retry; ghi kết quả gate gameplay và lỗi chưa giải quyết.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-25-dungeon-mvp.md. Thực hiện chỉ Phase 25 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 25, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

