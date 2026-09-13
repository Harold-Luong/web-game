# Phase 48 — Reconnect hoàn chỉnh

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | H — Hoàn thiện sản phẩm và mở rộng |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Grace period, khôi phục phiên và trạng thái; chốt cách xử lý hết thời gian chờ.

## Đầu vào và phụ thuộc

- [Phase 30 — Network resilience](phase-30-network-resilience.md).
- [Phase 36 — Server dungeon](phase-36-server-dungeon.md).
- [Phase 37 — Authentication](phase-37-authentication.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Nếu triển khai nhiều instance thì cần tích hợp routing Phase 47; nếu có loot/progression thì đối chiếu ledger Phase 40–43.

## Các bước thực hiện

1. Chốt grace period, trạng thái người mất mạng, slot giữ lại và hết hạn theo GDD.
2. Gắn reconnect với identity/session đúng; vô hiệu hóa kết nối cũ và trả full snapshot cùng sequence mới nhất.
3. Khôi phục player, dungeon, boss và kết quả đã ghi nếu có; xử lý reconnect sau trận kết thúc.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `server session/room restore`; `client reconnect UI`; `protocol snapshot phục hồi`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

AI thay người mặc định, phục hồi trận sau restart không có state hoặc room migration.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ thực hiện các hạng mục đã được giao và có điều kiện đầu vào. Không mở rộng hạ tầng/nội dung chỉ vì xuất hiện trong roadmap; ghi rõ phạm vi hệ thống thực tế.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Quay lại trong grace period điều khiển đúng player, không nhân bản entity hoặc thưởng.
- [ ] Token/identity không hợp lệ không chiếm được slot người khác.
- [ ] Hết grace period, room đã kết thúc hoặc server mất state có kết quả rõ ràng cho client.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Ngắt kết nối trong combat, lúc boss chết và sau kết quả; thử hai tab tranh reconnect, token cũ và hết grace period.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-48-reconnect.md. Thực hiện chỉ Phase 48 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 48, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

