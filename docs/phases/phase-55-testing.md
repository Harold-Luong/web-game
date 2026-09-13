# Phase 55 — Testing tổng thể

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | H — Hoàn thiện sản phẩm và mở rộng |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Combat, room, persistence, mô phỏng và tải; tình huống trùng yêu cầu/disconnect/cleanup/restart.

## Đầu vào và phụ thuộc

- [Phase 36 — Server dungeon](phase-36-server-dungeon.md).
- [Phase 44 — Difficulty](phase-44-difficulty.md).
- [Phase 48 — Reconnect hoàn chỉnh](phase-48-reconnect.md).
- [Phase 49 — Anti-cheat hardening](phase-49-anti-cheat-hardening.md).
- [Phase 54 — Performance](phase-54-performance.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Server restart có thể kết thúc trận nếu thiết kế chọn vậy; kiểm tra đúng cam kết phục hồi, không tự nâng yêu cầu.

## Các bước thực hiện

1. Lập ma trận rủi ro và phủ unit/integration/simulation/multiplayer-load cho chức năng đã có.
2. Bổ sung chỗ thiếu với seed/clock/fixture kiểm soát được, kiểm tra room isolation, cleanup và persistence.
3. Chạy bộ kiểm tra phù hợp, ghi lỗi có thể tái hiện, giới hạn môi trường và tiêu chí chặn phát hành.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `bộ test hiện có client/server`; `docs/quality/TEST-PLAN.md và báo cáo`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Viết test chỉ kiểm tên file, nâng tỷ lệ coverage bằng kiểm tra vô nghĩa hoặc hoãn mọi test trước đây tới phase này.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ thực hiện các hạng mục đã được giao và có điều kiện đầu vào. Không mở rộng hạ tầng/nội dung chỉ vì xuất hiện trong roadmap; ghi rõ phạm vi hệ thống thực tế.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Combat/cooldown, room và reward/inventory concurrency có kiểm tra tự động có ý nghĩa.
- [ ] Có kịch bản bốn người, disconnect lúc boss chết, skill spam, double request và restart server.
- [ ] Báo cáo phân biệt pass/fail/chưa chạy; lỗi ảnh hưởng kết quả trận hoặc dữ liệu không bị bỏ qua.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chạy từng lớp test trong môi trường được ghi và lặp lại kịch bản từng thất bại sau khi sửa; không gọi tải giả trong một room là kiểm thử nhiều room.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-55-testing.md. Thực hiện chỉ Phase 55 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 55, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

