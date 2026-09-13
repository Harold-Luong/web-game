# Phase 23 — Mini boss

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | D — Dungeon hoàn chỉnh |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Một mini boss có hai cơ chế, ví dụ Shield Knight.

## Đầu vào và phụ thuộc

- [Phase 03 — Boss mechanic design](phase-03-boss-mechanic-design.md).
- [Phase 21 — Dungeon architecture](phase-21-dungeon-architecture.md).
- [Phase 22 — Enemy variety](phase-22-enemy-variety.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Đặc tả mini boss phải khớp GDD/COMBAT; ghi rõ mechanic đề xuất trước khi làm nếu chưa có.

## Các bước thực hiện

1. Thiết kế ngắn một mini boss có hai cơ chế, ví dụ bait charge và phá enchantment của Shield Knight.
2. Tái dùng boss framework, aggro, shield và pipeline combat; bổ sung telegraph tối thiểu.
3. Nối encounter vào dungeon với bắt đầu/kết thúc/reset nhất quán.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/bosses/`; `cấu hình mini boss và room`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Boss framework mới, đủ bốn cơ chế như main boss, loot/progression hoặc art cuối.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Một dungeon tĩnh offline. Giữ các quy tắc class/boss đã thiết kế; chưa thêm Spring Boot, DB hoặc Redis.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Hai cơ chế đọc được và tạo cơ hội phối hợp, không chỉ tăng HP quái thường.
- [ ] Mini boss chết mở đường đúng một lần.
- [ ] Team wipe và retry không giữ shield/aggro/timer của lần trước.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chơi đúng cơ chế, bỏ lỡ cơ chế và team wipe rồi retry; kiểm tra cửa sau mini boss.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-23-mini-boss.md. Thực hiện chỉ Phase 23 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 23, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

