# Phase 50 — UI/UX

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | H — Hoàn thiện sản phẩm và mở rộng |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Lobby, HP, skill/cooldown, party, boss mechanic, kết quả và inventory rõ ràng.

## Đầu vào và phụ thuộc

- [Phase 36 — Server dungeon](phase-36-server-dungeon.md).
- [Phase 44 — Difficulty](phase-44-difficulty.md).
- [Phase 48 — Reconnect hoàn chỉnh](phase-48-reconnect.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Chỉ hiển thị chức năng thực sự tồn tại; không tạo nút giả cho phase chưa làm.

## Các bước thực hiện

1. Rà luồng vào phòng, chọn class, ready, dungeon, kết quả, reconnect và inventory đã tồn tại.
2. Hoàn thiện HP/party, skill/cooldown/resource, boss mechanic và trạng thái loading/error/empty.
3. Bố trí theo nền tảng đã chọn, làm tín hiệu đọc được, thao tác nhất quán và không che telegraph.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/ui/`; `lobby/HUD/results/inventory/settings presentation`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Đổi engine, thêm hệ gameplay mới, mobile chưa nằm trong GDD hoặc redesign art toàn bộ.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ thực hiện các hạng mục đã được giao và có điều kiện đầu vào. Không mở rộng hạ tầng/nội dung chỉ vì xuất hiện trong roadmap; ghi rõ phạm vi hệ thống thực tế.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Người chơi hiểu vai trò, skill sẵn sàng và nhiệm vụ mechanic hiện tại qua UI.
- [ ] Loading/lỗi/mất kết nối có trạng thái rõ; thao tác lặp không gửi hành động ngoài ý muốn.
- [ ] HUD/lobby/inventory đọc và thao tác được ở kích thước màn hình mục tiêu.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Đi xuyên suốt luồng chính, lỗi join, inventory trống/đầy và reconnect; kiểm tra các kích thước mục tiêu cùng bàn phím/chuột đã chọn.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-50-ui-ux.md. Thực hiện chỉ Phase 50 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 50, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

