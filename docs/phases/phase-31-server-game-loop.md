# Phase 31 — Server game loop

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | F — Server quyết định gameplay |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Vòng lặp nhận/kiểm tra lệnh, cập nhật mô phỏng và gửi snapshot/event; rõ quyền cập nhật room.

## Đầu vào và phụ thuộc

- [Phase 30 — Network resilience](phase-30-network-resilience.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Chốt thread model và chính sách quá tải trước code phụ thuộc; clock mô phỏng phải kiểm soát được khi test.

## Các bước thực hiện

1. Thiết kế một nơi sở hữu cập nhật state mỗi room, nhận lệnh qua hàng đợi thay vì sửa trực tiếp từ handler.
2. Implement tick theo thời gian cố định, xử lý command có giới hạn, cập nhật mô phỏng và phát snapshot/event.
3. Ghi chính sách tick chậm, lỗi trong một room, dừng/cleanup và metric thời gian tick tối thiểu.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-server/ — game loop, command queue, room lifecycle`; `docs/architecture/SERVER-LOOP.md`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Port toàn bộ combat/AI, DB trong tick loop hoặc hạ tầng nhiều server.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Server sở hữu kết quả trận. Client gửi intent và trình bày; không nhận damage, loot hoặc kết quả boss do client tự khai. Chưa thêm DB vào vòng lặp realtime.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Command được xử lý theo thứ tự/quy tắc đã định, không race khi nhiều kết nối gửi cùng lúc.
- [ ] Một room lỗi hoặc bị đóng không làm hỏng state room khác.
- [ ] Tick và scheduler được dọn khi room kết thúc; không tạo loop thứ hai khi start lặp.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Mô phỏng lệnh đồng thời, start/stop lặp và một tick chậm/lỗi; đo tick duration, không coi 20–30 tick/s là kết quả chưa đo.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-31-server-game-loop.md. Thực hiện chỉ Phase 31 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 31, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

