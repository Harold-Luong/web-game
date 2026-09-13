# Phase 24 — Full Golem

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | D — Dungeon hoàn chỉnh |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Hoàn thiện shield, crystal, stagger, adds và enrage theo thiết kế đã chốt.

## Đầu vào và phụ thuộc

- [Phase 03 — Boss mechanic design](phase-03-boss-mechanic-design.md).
- [Phase 20 — Class synergy](phase-20-class-synergy.md).
- [Phase 23 — Mini boss](phase-23-mini-boss.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Cơ chế bản solo Phase 14 chỉ giữ ở mode thử nếu còn cần; bản team phải theo Phase 3.

## Các bước thực hiện

1. Hoàn thiện shield/rune, shoulder crystal, stagger/core cùng các phase Golem đã thiết kế.
2. Bổ sung adds/enrage và chuyển phase theo ngưỡng/trigger đã chọn, hủy đòn cũ khi cần.
3. Đảm bảo telegraph, hướng boss và trạng thái điểm yếu quan sát được bởi cả đội mô phỏng.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/bosses/`; `cấu hình Golem team`; `UI mechanic tối thiểu`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Boss thứ hai, dungeon mới, network hoặc equipment.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Một dungeon tĩnh offline. Giữ các quy tắc class/boss đã thiết kế; chưa thêm Spring Boot, DB hoặc Redis.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Bốn vai trò tham gia chu kỳ boss và mọi phase đi đến kết quả được.
- [ ] Shield/crystal reset đúng khi đổi chu kỳ; không kích hoạt stagger lặp từ event cũ.
- [ ] Boss chết giữa cast/phase hoặc adds còn sống vẫn kết thúc theo luật thiết kế.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chơi toàn bộ boss team, vượt nhiều ngưỡng bằng một đòn, mất vai trò và chết lúc chuyển phase; kiểm tra không softlock.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-24-full-golem.md. Thực hiện chỉ Phase 24 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 24, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

