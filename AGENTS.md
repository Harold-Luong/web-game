# Hướng dẫn làm việc cho AI agent

## Phạm vi áp dụng

Áp dụng cho toàn bộ repository `web-game`. Đọc [README.md](README.md) trước khi thực hiện công việc để nắm yêu cầu, roadmap và quyết định còn mở. Giao tiếp và viết tài liệu bằng tiếng Việt; giữ nguyên tên công nghệ và định danh kỹ thuật khi cần.

Repository có **61 đặc tả phase riêng trong `docs/phases/`**, đánh số `phase-00-…md` đến `phase-60-…md`. Tên phase trong bảng roadmap của README liên kết trực tiếp tới file tương ứng. Khi được giao Phase N, đọc file đó cùng đầu ra thật của các phụ thuộc trước khi sửa.

## Trạng thái và giới hạn hiện tại

**Hiện tại chỉ làm tài liệu, chưa tạo code.** Người dùng yêu cầu đọc cuộc trò chuyện và chuẩn bị README/AGENTS để làm việc với dự án.

- Được tạo, sửa và kiểm tra tài liệu Markdown trong phạm vi yêu cầu.
- Chưa tạo source code, scaffold client/server, manifest dependency, lockfile, cấu hình build/runtime/CI, migration, container hoặc script triển khai.
- Chưa cài package, tạo asset game, khởi chạy dịch vụ hoặc deploy trong nhiệm vụ tài liệu này.
- Các cấu trúc thư mục, công nghệ và phase trong README là kế hoạch, không chứng minh tính năng đã tồn tại.
- Khi người dùng giao nhiệm vụ triển khai rõ ràng ở lượt sau, nhiệm vụ đó cho phép làm code trong phạm vi được giao. Không yêu cầu một câu xác nhận bổ sung chỉ để gỡ giới hạn của nhiệm vụ tài liệu trước đó; cập nhật trạng thái tài liệu tương ứng.

## Bảo toàn ý định sản phẩm

- Game web 2D co-op cho 4 người: Tank, Mage, Archer, Warrior; mỗi vai trò có cơ chế riêng để phối hợp vượt dungeon và xử lý điểm yếu boss.
- Không tự đổi thành game solo, chỉ có ba class, PvP hoặc open world. Prototype Warrior solo và mô phỏng offline chỉ là bước kiểm chứng cho sản phẩm co-op.
- Phân biệt yêu cầu người dùng với đề xuất từ câu trả lời AI trong nguồn. Tên Dungeon Bonds, Ancient Golem, stack và thông số thiết kế là cơ sở review cho đến khi được chốt.
- Lấy roadmap cuối trong README làm hệ đánh số: 8 nhóm A–H, Phase 0–60. Không dùng lẫn roadmap cũ 0–25 hoặc con số “36 phase” bị sai trong nguồn.
- Các skill được liệt kê là tham khảo; chọn bộ tối thiểu theo thiết kế đã chốt, không triển khai toàn bộ danh sách ngay.
- Ưu tiên offline gameplay → 4 class/dungeon → multiplayer → server authoritative → persistence/progression → production. Không kéo login, DB, Redis hoặc matchmaking vào prototype.

## Quy trình cho mỗi nhiệm vụ

1. Đọc README, hướng dẫn áp dụng và trạng thái repository. Kiểm tra thay đổi đang có để không ghi đè công việc của người dùng.
2. Xác định phase hoặc hạng mục được giao, đầu vào đã có và phụ thuộc còn thiếu. Tài liệu mô tả tính năng không đồng nghĩa tính năng đã được triển khai.
3. Làm rõ phạm vi, đầu ra và cách kiểm chứng trước khi sửa. Tự quyết các chi tiết nhỏ, có thể đảo ngược trong phạm vi được giao; ghi giả định có ảnh hưởng. Chỉ hỏi khi thông tin thiếu làm thay đổi đáng kể gameplay, kiến trúc hoặc phạm vi và không thể suy ra từ ngữ cảnh.
4. Hoàn thành công việc được giao và các chỉnh sửa cần thiết để kết quả nhất quán. Mặc định mỗi nhiệm vụ là một phase; nếu người dùng giao nhiều phase thì thực hiện phạm vi đó. Không tự làm phase kế tiếp hoặc refactor phần không liên quan.
5. Kiểm chứng bằng cách phù hợp với thay đổi. Nếu thiếu môi trường hoặc asset, nêu rõ điều chưa kiểm chứng; không tự đánh dấu đạt.
6. Cập nhật tài liệu về hành vi, quyết định và tiến độ thực tế. Báo kết quả, các file thay đổi, tiêu chí đạt/chưa đạt và công việc còn lại thuộc phạm vi nhiệm vụ.

Review gate là điểm đánh giá bằng chứng gameplay/kỹ thuật, không phải mặc định phải hỏi quyền sau từng file hoặc thao tác. Nếu phạm vi tiếp theo đã được người dùng giao và các điều kiện đã đáp ứng, tiếp tục thực hiện. Nếu chưa được giao, chỉ ghi bước tiếp theo, không tự triển khai.

### Mẫu giao việc theo phase

| Trường | Nội dung cần có |
| --- | --- |
| Phase / Goal | Mã phase trong README và hành vi cần đạt |
| Dependencies | Mốc/tài liệu/chức năng phải có trước khi thực hiện |
| Scope | Các thay đổi và phạm vi file dự kiến |
| Non-goals | Tính năng hoặc phase chưa làm trong nhiệm vụ này |
| Architecture constraints | Ranh giới scene/system, client/server và dữ liệu có liên quan |
| Deliverables | Tài liệu, tính năng hoặc cấu hình cụ thể tùy giai đoạn được giao |
| Acceptance criteria | Kết quả có thể quan sát và đánh giá, không chỉ tên file tồn tại |
| Verification | Kiểm tra thủ công, test, build hoặc bằng chứng phù hợp |

Đây là khung mô tả task, không phải yêu cầu tạo thêm file cho mọi thao tác nhỏ.

### Sử dụng các file phase

- Mỗi phase có đúng một file giao việc. Giữ nguyên mã 00–60 và ưu tiên cập nhật file hiện có; không tạo thêm bản đặc tả/checklist trùng cho cùng phase.
- File phase là nhiệm vụ cần làm, không phải đầu ra đã hoàn tất. Ví dụ file Phase 00 mô tả cách viết GDD; GDD chỉ tồn tại sau khi nhiệm vụ thiết kế được thực hiện.
- Các file/thành phần nêu trong mục đầu ra là dự kiến. Kiểm tra cấu trúc thực tế và tái dùng module hiện có; không tạo mọi thư mục tương lai từ danh sách đó.
- Checklist ban đầu phải để trống. Chỉ đánh dấu tiêu chí có bằng chứng, ghi kết quả ở mục “Báo cáo sau khi thực hiện” và giữ trạng thái ở bảng đầu file nhất quán.
- Dùng `NOT_STARTED`, `IN_PROGRESS`, `BLOCKED`, `DONE`, `DEFERRED` để mô tả công việc. `BLOCKED` cần nêu phụ thuộc/thông tin cụ thể còn thiếu; `DEFERRED` dành cho hạng mục có điều kiện chưa được chọn, không tính như `DONE`.
- Phụ thuộc trong file là các mốc chính; vẫn đọc roadmap tổng thể và kiểm tra thay đổi thực tế. Không tự làm nhiều phase chỉ vì một phụ thuộc chưa tồn tại.
- Nếu thay đổi thiết kế ảnh hưởng phase khác, cập nhật phần mô tả và liên kết liên quan trong phạm vi nhiệm vụ; không tự triển khai các phase đó.
- Khi người dùng chỉ yêu cầu tạo/review file phase, giữ toàn bộ công việc ở tài liệu. Mẫu lệnh thực hiện nằm trong tài liệu không phải chỉ thị tự chạy trong lượt hiện tại.

## Nguyên tắc khi được giao triển khai

### Client, combat và asset

- Dùng TypeScript/Vite/Phaser theo định hướng hiện tại nếu người dùng không đổi stack; xác định phiên bản tương thích khi bootstrap.
- Giữ scene tập trung điều phối. Tách entity, skill, combat, enemy AI, boss và dungeon theo nhu cầu thực tế; ưu tiên composition, không dựng framework tổng quát trước khi có nhu cầu.
- Đưa stat và skill definition ra dữ liệu/cấu hình phù hợp. Damage phải đi qua pipeline chung; không sửa HP rải rác trong input hoặc scene.
- Phân biệt hitbox/hurtbox; kiểm soát thời điểm đánh trúng, số lần hit trong một lần tấn công và trạng thái chết. Quy tắc multi-hit phải được nêu rõ theo skill.
- Animation không restart mỗi frame. Hit timing cần khớp hình ảnh; khi có server, kết quả gameplay do mô phỏng server quyết định.
- Bắt đầu bằng placeholder. Không tự tạo hình, mua asset hoặc đổi art style nếu task không bao gồm phần đó. Concept sheet từ cuộc trò chuyện chưa phải asset trong repository.
- Khi thêm asset, ghi nguồn/điều kiện sử dụng, frame size, điểm neo và cách đặt tên đủ để người khác dùng lại.

### Multiplayer và server

- Nhóm E bắt đầu với Spring Boot/WebSocket và room trong bộ nhớ; chưa thêm DB chỉ để làm create/join/ready.
- Định nghĩa protocol trước khi mở rộng xử lý message. Thống nhất type/version, input, sequence và quy tắc lỗi; không để các tên message khác nhau trong bản thảo trở thành contract mâu thuẫn.
- Client gửi intent. Server kiểm tra quyền tham gia room, trạng thái sống/chết, movement, cooldown, tài nguyên nếu có, range và hit. Không tin damage, HP, loot hoặc phần thưởng do client tự khai.
- Server sở hữu AI, boss state và điều kiện dungeon khi đến nhóm F. Client trình bày state cùng prediction/interpolation theo thiết kế.
- Có cơ chế sở hữu/cập nhật room rõ ràng để xử lý đồng thời; tránh WebSocket handler tùy ý sửa chung game state. Thiết kế thread model ở phase phù hợp.
- Bảo đảm room isolation, disconnect handling và cleanup; không triển khai AI thay người chơi hoặc cơ chế reconnect chưa được chốt chỉ vì nguồn có gợi ý.
- Các thông số như 20–30 tick/giây là điểm xuất phát cần đo, không báo thành cam kết hiệu năng.

### Persistence và hạ tầng

- Nhóm G mới đưa vào tài khoản, PostgreSQL/JPA và tiến trình. Chỉ lưu dữ liệu bền vững; không ghi tọa độ, projectile hoặc HP quái từng tick vào DB.
- Loot do server xác định. Inventory/reward cần transaction, constraint và chiến lược chống xử lý lặp/concurrency phù hợp; client chỉ hiển thị kết quả đã được chấp nhận.
- Redis chỉ thêm khi có nhu cầu cụ thể; không dùng thay database inventory. Multi-instance chỉ khi có yêu cầu và bằng chứng cần scale; mỗi room có một instance sở hữu.
- Không tự thêm microservice, queue, Kubernetes hoặc hệ thống kinh tế ngoài scope.

## Kiểm chứng và tiêu chí hoàn thành

### Khi chỉ sửa tài liệu

- Kiểm tra liên kết nội bộ, tiếng Việt UTF-8, mã phase, số lượng phase và sự nhất quán README/AGENTS.
- Phân biệt rõ hiện trạng với dự kiến, yêu cầu đã chốt với đề xuất; không viết lệnh chạy hoặc kết quả test như thể ứng dụng đã tồn tại.
- Kiểm tra diff/status để bảo đảm chỉ có file tài liệu trong phạm vi yêu cầu thay đổi.
- Không tạo test, dependency hoặc source chỉ để kiểm tra Markdown.

### Khi có code trong nhiệm vụ sau

- Dùng các lệnh build/typecheck/test thực sự có trong repository, ghi lại lệnh đã chạy và kết quả. Chưa có công cụ thì nói rõ; không bịa `npm test` hoặc khẳng định build pass.
- Thay đổi tương tác cần kiểm tra trong browser khi công cụ cho phép. Kiểm tra điều khiển, va chạm, animation, hit timing và thắng/thua phù hợp với phase; nếu chưa thể chạy browser, nêu giới hạn đó.
- Viết test có giá trị cho công thức combat, trạng thái/cooldown, protocol/room và giao dịch dữ liệu khi các phần này được triển khai. Không đợi đến Phase 55 mới kiểm tra chất lượng.
- Với multiplayer, kiểm tra bốn client, room isolation, disconnect và yêu cầu không hợp lệ ở phase liên quan. Với loot/inventory, kiểm tra yêu cầu trùng, thao tác đồng thời và trường hợp disconnect khi nhận thưởng.
- Một phase chỉ hoàn tất khi đầu ra và acceptance criteria có bằng chứng. Không đánh dấu milestone hoàn thành chỉ vì có scaffold hoặc tài liệu mô tả.

### Báo cáo kết quả

Trình bày ngắn gọn: đã thay đổi gì và vì sao; file đã tạo/sửa; cách kiểm chứng và kết quả; giới hạn hoặc quyết định còn mở. Không báo tính năng đã chạy, test đã pass hoặc phase đã xong nếu chưa có bằng chứng. Không tự commit, push hay deploy nếu nhiệm vụ không bao gồm các hành động đó.
