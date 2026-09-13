# Phase 27 — Network protocol

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | E — Nền tảng multiplayer |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Contract, version, payload, sequence, validation và lỗi được thống nhất.

## Đầu vào và phụ thuộc

- [Phase 26 — Server bootstrap](phase-26-server-bootstrap.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Chốt đơn vị tọa độ/thời gian, cách cấp identity tạm và ràng buộc room; auth tài khoản tới Phase 37.

## Các bước thực hiện

1. Định nghĩa envelope, version, type, sequence, thời gian và quy tắc identity/room membership.
2. Chốt message create/join/leave/ready/move/use-skill/interact và snapshot/event/error cần cho MVP; mô tả payload và đơn vị.
3. Đồng bộ contract hai phía, kiểm tra parser/validation và version không hỗ trợ; phân biệt snapshot với event.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `docs/network/PROTOCOL.md`; `kiểu message/validation client và server`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Mọi handler gameplay, binary protocol tối ưu sớm, DB hoặc microservice.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Server đầu tiên dùng state trong bộ nhớ. Định danh phiên tạm không phải tài khoản bền vững; chưa coi đồng bộ movement là gameplay authoritative hoàn chỉnh.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Một loại hành động có một tên và cấu trúc thống nhất giữa client/server.
- [ ] Payload thiếu/sai kiểu/quá giới hạn hoặc type/version lạ có lỗi rõ, không crash handler.
- [ ] MOVE/USE_SKILL thể hiện intent; không nhận damage/loot từ client làm sự thật.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chạy cùng bộ payload hợp lệ và sai qua parser hai phía; kiểm tra sequence trùng/cũ theo luật contract.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-27-network-protocol.md. Thực hiện chỉ Phase 27 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 27, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

