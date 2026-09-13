# Phase 41 — Inventory

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | G — Tài khoản và progression |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Thêm/xóa/trang bị/tháo, bảo đảm tính nhất quán khi thao tác đồng thời.

## Đầu vào và phụ thuộc

- [Phase 40 — Loot system](phase-40-loot-system.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Chốt stack/capacity và cách xử lý reward khi đầy; không bỏ mất reward ledger nếu chưa giao item thành công.

## Các bước thực hiện

1. Định nghĩa slot, stack, sức chứa và ownership; gắn reward đã ghi vào inventory theo thao tác có tính lặp an toàn.
2. Implement add/remove và yêu cầu equip/unequip ở mức trạng thái sở hữu; Phase 42 mới tính tác động stat trang bị.
3. Dùng transaction, constraint và cơ chế concurrency để cập nhật không mất item/nhân item.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-server/ — inventory/item definition/item instance`; `schema/API`; `client inventory tối thiểu`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Trading, auction, crafting, stat bonus equipment hoặc UI hoàn thiện.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Phân biệt persistent state với state trong RAM của trận. Mọi thay đổi dữ liệu có ownership và tính nhất quán; không đưa truy cập DB vào mỗi tick.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Reward được đưa vào inventory đúng một lần, kể cả gọi lại sau disconnect.
- [ ] Thao tác vượt số lượng/sức chứa hoặc dùng item của người khác bị từ chối đúng.
- [ ] Hai thao tác đồng thời không tạo số lượng âm, duplicate item hoặc lost update.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Nhận cùng reward hai lần, inventory đầy, remove/equip đồng thời và truy cập chéo tài khoản; kiểm tra rollback khi lỗi.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-41-inventory.md. Thực hiện chỉ Phase 41 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 41, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

