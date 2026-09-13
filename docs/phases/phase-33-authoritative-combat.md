# Phase 33 — Authoritative combat

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | F — Server quyết định gameplay |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Server kiểm tra skill, cooldown, state, range, hit và tính damage.

## Đầu vào và phụ thuộc

- [Phase 01 — Combat design](phase-01-combat-design.md).
- [Phase 02 — Class design](phase-02-class-design.md).
- [Phase 10 — Damage system](phase-10-damage-system.md).
- [Phase 32 — Authoritative movement](phase-32-authoritative-movement.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Skill unlocked ở giai đoạn này theo cấu hình phiên; persistence/unlock tài khoản thuộc nhóm G.

## Các bước thực hiện

1. Port quy tắc skill/cooldown/hit/damage sang mô phỏng server với cùng dữ liệu thiết kế.
2. Validate room, quyền điều khiển, alive/state, skill, resource, range và sequence trước khi nhận cast.
3. Server cập nhật HP/death một lần rồi broadcast kết quả; client hiển thị hiệu ứng mà không tự quyết damage.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-server/ — skills/combat/status`; `client combat events`; `contract`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Enemy AI đầy đủ, loot, tài khoản unlock bền vững hoặc client xác nhận hit như kết quả chính thức.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Server sở hữu kết quả trận. Client gửi intent và trình bày; không nhận damage, loot hoặc kết quả boss do client tự khai. Chưa thêm DB vào vòng lặp realtime.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Payload damage/HP giả, skill lạ, spam cooldown hoặc thao tác ngoài room không gây tác động trái luật.
- [ ] Ví dụ tính damage client offline và server khớp thiết kế, kể cả shield/overkill.
- [ ] Hai người đánh cùng mục tiêu không tạo hai death event hoặc HP dưới giới hạn.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chạy bộ ví dụ COMBAT trên server, gửi cast sai/trùng và hai hit cùng tick; quan sát HP nhất quán giữa bốn client.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-33-authoritative-combat.md. Thực hiện chỉ Phase 33 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 33, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

