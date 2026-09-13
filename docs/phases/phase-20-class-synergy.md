# Phase 20 — Class synergy

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | C — Bốn class và phối hợp |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Bốn entity cùng tham gia combat; mô phỏng offline bằng debug input/chuyển điều khiển hoặc AI đơn giản, kiểm chứng chu kỳ phối hợp.

## Đầu vào và phụ thuộc

- [Phase 16 — Tank](phase-16-tank.md).
- [Phase 17 — Mage](phase-17-mage.md).
- [Phase 18 — Archer](phase-18-archer.md).
- [Phase 19 — Warrior hoàn thiện](phase-19-warrior-finalization.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Cách điều khiển mô phỏng chỉ là công cụ kiểm chứng, không thay yêu cầu đội bốn người của sản phẩm.

## Các bước thực hiện

1. Spawn bốn class trong cùng encounter bằng chuyển điều khiển/debug input hoặc AI tối thiểu có phạm vi.
2. Nối aggro → rune shield → crystal → stagger/core theo luật boss, cho phép chuỗi không tuyến tính nếu thiết kế chọn vậy.
3. Kiểm tra nhiều player cùng gây hit, class chết/thiếu và kết thúc/reset encounter.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/bosses/`; `scene mô phỏng bốn class`; `công cụ debug tối thiểu`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Network, sản phẩm chơi solo với bot, AI đồng đội đầy đủ hoặc dungeon mới.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Kiểm chứng bốn vai trò bằng mô phỏng offline. Dùng composition và pipeline combat chung, không tạo sản phẩm solo với hệ bot đầy đủ.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Bốn class cùng tồn tại với ID, HP và cooldown riêng, đánh cùng boss không lỗi state.
- [ ] Mỗi vai trò có tác động riêng và chu kỳ phối hợp hoàn thành được offline.
- [ ] Mất một vai trò hoặc hụt mechanic dẫn đến kết quả đã thiết kế, không kẹt state vô hạn.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Chạy chu kỳ phối hợp thành công, bỏ qua từng vai trò và hai đòn cùng tick; ghi quan sát về đóng góp từng class cho M3.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-20-class-synergy.md. Thực hiện chỉ Phase 20 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 20, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

