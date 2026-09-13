# Phase 18 — Archer

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | C — Bốn class và phối hợp |
| Trạng thái công việc | NOT_STARTED — mới có đặc tả giao việc |
| Loại nhiệm vụ | Triển khai/kiểm chứng khi người dùng giao phase |

Đây là tài liệu để giao việc cho AI, chưa phải tính năng hoặc thiết kế đã hoàn tất. Việc tạo file này không cho phép tự bắt đầu code. Khi được giao thực hiện phase, làm theo phạm vi bên dưới và hướng dẫn gốc; không cần xin lại quyền cho các bước đã nằm trong nhiệm vụ.

## Mục tiêu

Bắn tầm xa, phát hiện hit ở bộ phận và xử lý weakpoint.

## Đầu vào và phụ thuộc

- [Phase 02 — Class design](phase-02-class-design.md).
- [Phase 15 — Character architecture](phase-15-character-architecture.md).
- [Phase 17 — Mage](phase-17-mage.md).

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Điểm cần xử lý trước phần phụ thuộc:** Quy tắc ưu tiên body/weakpoint và class được phép phá phải lấy từ Phase 3.

## Các bước thực hiện

1. Tạo Archer với bộ skill MVP; tái dùng projectile thay vì tạo đường damage riêng.
2. Định nghĩa bộ phận/weakpoint có ID, hurtbox, trạng thái active/destroyed và liên hệ với boss.
3. Cho phép ngắm/bắn crystal theo thiết kế; quy định hit body và hit weakpoint khi vùng chồng nhau.

## Đầu ra và phạm vi file

- Đường dẫn/thành phần dự kiến: `game-client/src/skills/`; `cấu hình Archer`; `projectile và weakpoint`.
- Đây là gợi ý vị trí, chưa phải file hiện có. Kiểm tra cấu trúc thật trước khi tạo; ưu tiên sửa phần tương ứng đã tồn tại thay vì tạo bản thứ hai.
- Bàn giao thay đổi phục vụ mục tiêu trên, ghi quyết định ảnh hưởng hành vi và kết quả kiểm chứng ngay trong phần báo cáo cuối file này. Chỉ cập nhật tài liệu gốc khi có thay đổi liên quan.

## Không làm trong phase này

Mọi skill Archer, auto-aim phức tạp, mục tiêu bay toàn dungeon hoặc network.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Kiểm chứng bốn vai trò bằng mô phỏng offline. Dùng composition và pipeline combat chung, không tạo sản phẩm solo với hệ bot đầy đủ.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [ ] Mũi tên chỉ trúng vùng hợp lệ theo hướng/tầm và vòng đời projectile.
- [ ] Crystal nhận hit độc lập với body theo luật, bị phá một lần và báo về boss.
- [ ] Bộ phận đã phá không tiếp tục kích hoạt stagger hoặc phát thưởng sự kiện.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Bắn body, crystal, điểm rìa/chồng vùng, crystal đã phá và projectile hết hạn; kiểm tra không double-hit ngoài thiết kế.

Dùng lệnh build/typecheck/test thực sự có ở thời điểm triển khai và phù hợp với phần thay đổi. Ghi lệnh, môi trường và kết quả; nếu browser, database, người chơi thử hoặc hạ tầng chưa sẵn sàng thì ghi phần chưa kiểm chứng.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-18-archer.md. Thực hiện chỉ Phase 18 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 18, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: NOT_STARTED.
- Quyết định/giả định đã chốt: chưa có trong lần thực hiện phase.
- File thực tế đã tạo/sửa: chưa thực hiện.
- Kiểm chứng, môi trường và kết quả: chưa chạy.
- Tiêu chí chưa đạt / điểm còn chờ: toàn bộ checklist phía trên.
- Bàn giao cho phase sau: chưa có; không tự bắt đầu phase tiếp theo.

