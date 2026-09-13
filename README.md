# web-game

Game web 2D co-op vượt dungeon dành cho đội 4 người: **Đỡ đòn (Tank), Pháp sư (Mage), Cung thủ (Archer), Chiến binh (Warrior)**. Trọng tâm là phối hợp giải quyết cơ chế boss, với điểm yếu và thời điểm hành động riêng cho từng vai trò.

**Trạng thái: chuẩn bị thiết kế, chỉ có tài liệu; chưa triển khai code.** Chưa có ứng dụng chạy được, dependency, lệnh cài đặt, build hoặc test.

## Nguồn và cách đọc

Tài liệu được tổng hợp từ [cuộc trò chuyện “Xây dựng web game 2D”](https://chatgpt.com/share/6aa69e1d-b684-83ec-ae04-07e145234c7f), đọc ngày 13/09/2026, và yêu cầu hiện tại chỉ viết tài liệu.

- **Yêu cầu đã xác nhận:** game web 2D; đội 4 người với 4 vai trò nêu trên; cùng vượt ải; boss có điểm yếu để mỗi vai trò phát huy sức mạnh; chia công việc theo phase để review và giao cho AI từng bước.
- **Đề xuất làm cơ sở review:** stack, thứ tự triển khai, Ancient Golem, danh sách skill, thiết kế dungeon và kiến trúc bên dưới được tổng hợp từ các câu trả lời trong cuộc trò chuyện. Đây chưa phải toàn bộ quyết định đã được người dùng chốt.
- **Chưa chốt:** được tập hợp ở cuối tài liệu. Không tự biến gợi ý thành yêu cầu bắt buộc.

Cuộc trò chuyện có nhiều roadmap. Tài liệu này dùng bản tổng thể cuối cùng với **8 nhóm A–H, 61 phase đánh số 0–60**. Cụm “36 phase nhỏ” ở phần mở đầu nguồn không khớp danh sách thực tế; các số phase của roadmap cũ không được dùng lẫn với bản này.

| Tài liệu | Mục đích |
| --- | --- |
| [README.md](README.md) | Bối cảnh sản phẩm, phạm vi, kiến trúc dự kiến, roadmap và các điểm cần quyết định |
| [AGENTS.md](AGENTS.md) | Quy tắc làm việc cho AI agent, giới hạn từng phase và cách kiểm chứng kết quả |
| `docs/phases/phase-00-…md` đến `phase-60-…md` | 61 file giao việc riêng; mở từng file từ bảng roadmap bên dưới |

## Định hướng sản phẩm

Đội hình mục tiêu gồm một người cho mỗi vai trò. Khác biệt giữa class cần thể hiện qua hành động, vị trí và khả năng xử lý cơ chế; chỉ thay màu nhân vật hoặc hệ số sát thương là chưa đủ.

Vòng chơi dự kiến: vào lobby → chọn class và lập đội → vào dungeon → dọn quái → mini boss → boss chính → thắng/thua. Khi đến giai đoạn progression, bổ sung nhận thưởng → nâng cấp → thử dungeon khó hơn.

Tên repository hiện tại là `web-game`. **Dungeon Bonds** là tên được gợi ý trong nguồn, chưa phải tên sản phẩm chính thức. Góc nhìn top-down và phong cách fantasy cartoon/pixel-ish cũng đang là đề xuất.

### Vai trò và phối hợp

| Class | Công việc trong đội | Cơ chế để thể hiện vai trò | Skill tham khảo, chưa phải bộ skill đã chốt |
| --- | --- | --- | --- |
| Tank | Giữ tuyến đầu, bảo vệ và tạo khoảng trống | Giữ aggro, xoay hướng boss, chặn đòn đúng lúc | Shield Block, Taunt, Ground Slam, Fortify |
| Mage | Xử lý cơ chế phép và kiểm soát nhóm quái | Phá rune/khiên phép, AoE và hiệu ứng khống chế | Magic Bolt, Fireball, Ice Nova, Arcane Break, Blink |
| Archer | Đánh chính xác từ xa và ưu tiên mục tiêu | Bắn crystal, bộ phận nhỏ hoặc khó tiếp cận | Basic Arrow, Charged Shot, Trap, Rain of Arrows, Weakpoint Shot |
| Warrior | Cận chiến, phá giáp và dồn sát thương | Tận dụng thời gian boss bị stagger hoặc lộ lõi | Slash Combo, Heavy Slash, Leap, Armor Break, Execute |

Nguyên tắc thiết kế: Tank có quyết định chủ động; Mage có việc ngoài spam AoE; Archer có điểm yếu thực sự để ngắm; Warrior có cửa sổ dồn sát thương rõ ràng. Không đo đóng góp của mọi class chỉ bằng tổng damage.

### Boss đầu tiên: Ancient Golem — đề xuất

Golem đá có rune bảo vệ, crystal ở vai và lõi ở ngực. Chu kỳ minh họa:

1. Tank giữ hướng boss và xử lý đòn nguy hiểm.
2. Mage phá lớp rune shield.
3. Archer phá crystal để mở trạng thái stagger.
4. Warrior áp sát lõi và dồn sát thương trong thời gian lộ điểm yếu.
5. Boss hồi phục hoặc chuyển phase, đội tiếp tục xử lý chu kỳ mới.

Đòn tấn công cần báo trước bằng dấu hiệu dễ đọc, có thời gian phản ứng rồi mới gây tác động. Prototype có thể dùng punch, ground slam, charge và shockwave. Bản đầy đủ có thể thêm shield, quái triệu hồi và enrage.

Chu kỳ trên là ví dụ phối hợp, chưa chốt thành chuỗi bắt buộc tuyệt đối. Cần quyết định cách xử lý khi thiếu người, một class chết hoặc thao tác cơ chế thất bại để tránh trận đấu bị kẹt. Nhện Chúa và Rồng Bão trong nguồn là ý tưởng mở rộng, không thuộc dungeon đầu tiên.

## Phạm vi theo mốc

| Mốc | Có trong phạm vi | Chưa làm tại mốc này |
| --- | --- | --- |
| Thiết kế hiện tại | Tổng hợp yêu cầu, review gameplay, kiến trúc và roadmap | Code, scaffold, cài dependency, tạo asset, backend, triển khai |
| Vertical slice offline | Một Warrior, di chuyển, animation cơ bản, combat, một loại quái, phòng chiến đấu, Golem đơn giản, thắng/thua | Multiplayer, tài khoản, DB, inventory, Redis |
| Dungeon offline | 4 class, kiểm thử phối hợp tại máy, một dungeon tĩnh, mini boss và Golem có cơ chế | Network, progression bền vững, nhiều dungeon |
| Multiplayer MVP | Lobby/room cho 4 người, chọn class, ready/start, đồng bộ, server quyết định gameplay, thắng/thua, xử lý mất kết nối cơ bản | Matchmaking tự động, kinh tế phức tạp, hạ tầng nhiều máy chủ |
| Progression | Tài khoản, lưu nhân vật, loot, inventory, equipment, EXP/level, độ khó | Trading, auction house, hệ thống kinh tế mở rộng |
| Production và mở rộng | UI/art/audio hoàn thiện, kiểm thử tải, quan sát vận hành, deploy; Redis/scaling khi có nhu cầu | Không mặc định thực hiện mọi ý tưởng chỉ vì có trong roadmap |

Ngoài MVP: PvP, guild, open world, trading, auction house, crafting phức tạp, thế giới procedural lớn, talent tree và nội dung theo mùa.

Đề xuất thu nhỏ bộ kỹ năng ban đầu thành **đánh thường + 2 skill mỗi class**; passive và bộ skill đầy đủ sẽ được chốt trong Phase 2. Hai skill được chọn phải hỗ trợ vai trò cơ chế của class. Các danh sách 4–5 skill trong nguồn là hướng phát triển, không phải yêu cầu làm tất cả ngay.

Dungeon đầu tiên dự kiến: phòng bắt đầu → hai phòng chiến đấu → mini boss → phòng nghỉ → Golem → kết quả. Các mốc 5–10, 10–20 và 15–30 phút xuất hiện ở những đề xuất khác nhau; **chưa có thời lượng chính thức**. Có thể dùng 10–20 phút làm giả thuyết cho dungeon đầu để kiểm chứng khi chơi thử.

## Kiến trúc dự kiến

Ưu tiên kiểm chứng gameplay offline, sau đó multiplayer, rồi mới tài khoản và lưu tiến trình. Bắt đầu với một ứng dụng server; chưa tách microservice.

| Thành phần | Công nghệ đề xuất | Thời điểm và trách nhiệm |
| --- | --- | --- |
| Game client | TypeScript, Vite, Phaser | Nhóm B; input, scene, sprite, animation, camera, âm thanh và UI |
| Game server | Java, Spring Boot, WebSocket | Nhóm E–F; room, mô phỏng trận đấu, kiểm tra lệnh và đồng bộ |
| API và tài khoản | Spring Security, HTTP API | Nhóm G; đăng nhập, hồ sơ và dữ liệu ngoài vòng lặp realtime |
| Lưu dữ liệu | PostgreSQL, Spring Data JPA | Nhóm G; nhân vật, tiến trình, inventory, equipment |
| Cache và điều phối | Redis | Nhóm H nếu cần presence, tra cứu room, queue, leaderboard hoặc cache |
| Đóng gói và phục vụ | Docker, Nginx | Giai đoạn triển khai; phục vụ client và chuyển tiếp API/WebSocket |

Chưa khóa phiên bản Node.js, Java, Phaser, Spring Boot hoặc công cụ build Java. Khi bắt đầu phase triển khai liên quan, kiểm tra tương thích rồi ghi phiên bản và lệnh thực tế vào tài liệu.

### Ranh giới logic

- Scene điều phối các thành phần; tách movement, combat, skill, status, AI và dungeon thành các phần có trách nhiệm rõ ràng. Ưu tiên composition, tránh cây kế thừa sâu hoặc sao chép nguyên class Warrior.
- Dữ liệu entity tối thiểu dự kiến: định danh, vị trí, HP, trạng thái và còn sống/chết. Chỉ thêm abstraction phục vụ phase hiện tại.
- Skill có định nghĩa riêng cho cooldown, cast time, tầm đánh, hệ số damage và hitbox. Hitbox là vùng gây tác động; hurtbox là vùng nhận tác động.
- Damage đi qua một pipeline: hành động → phát hiện hit → yêu cầu damage → tính kết quả → cập nhật HP → phát sự kiện. Công thức khởi điểm đề xuất: sát thương bằng giá trị lớn hơn giữa sát thương tối thiểu và attack nhân hệ số skill trừ defense. Quy tắc làm tròn, sát thương tối thiểu và tương tác shield chưa chốt.
- Các stat dự kiến: HP, Attack, Defense, MoveSpeed, AttackSpeed, CooldownReduction. Trạng thái tham khảo: NORMAL, STUN, SLOW, SHIELDED, INVULNERABLE, STAGGERED, DEAD; cần xác định cách kết hợp và ưu tiên trong thiết kế combat.
- Animation thể hiện hành động; thời điểm hiệu lực của hit phải khớp thao tác. Ở multiplayer, server quyết định thời điểm và kết quả combat, không phụ thuộc event animation do client báo về.

### Multiplayer và dữ liệu

Client gửi ý định di chuyển, dùng skill và tương tác. Server kiểm tra người chơi, trạng thái, cooldown, tài nguyên nếu có, tầm đánh và va chạm; sau đó quyết định vị trí, HP, AI, boss, dungeon và phần thưởng. Không nhận damage hoặc loot do client tự tính làm kết quả chính thức.

Phase 27 sẽ thiết kế contract có type, version, sequence và quy tắc payload. Các nhóm message tham khảo gồm vào phòng/ready, di chuyển/dùng skill/tương tác, trạng thái room/player/entity, spawn/death, damage và trạng thái boss. Tên MOVE, MOVE_DIRECTION và MOVE_START/MOVE_STOP trong các bản thảo nguồn cần được thống nhất trước khi triển khai protocol.

Server tick 20–30 lần/giây là giả thuyết ban đầu để đo, không phải thông số đã kiểm chứng. Remote player dùng interpolation; prediction và reconciliation cho người chơi cục bộ được bổ sung theo phase. Mỗi room có nơi sở hữu và cập nhật trạng thái rõ ràng; mô hình thread cụ thể cần được thiết kế trước vòng lặp server.

Trạng thái trận đấu thay đổi liên tục nằm trong bộ nhớ game server: vị trí, projectile, HP quái và trạng thái boss. PostgreSQL lưu dữ liệu bền vững như tài khoản, nhân vật, EXP, item và tiến trình; không ghi vị trí từng tick. Loot/inventory cần transaction, ràng buộc dữ liệu và xử lý yêu cầu trùng để không phát thưởng hoặc nhân bản item hai lần. Redis không thay vai trò database inventory và không bắt buộc cho server đầu tiên.

### Asset và animation

Ưu tiên placeholder trong prototype. Concept nhân vật được tạo trong cuộc trò chuyện chỉ là tham khảo thị giác; repository hiện chưa có hình đó hoặc sprite sheet dùng được.

Hướng đề xuất là sprite sheet: idle, run, attack, hurt, death; skill animation thêm khi cần. Kích thước 64×64 hoặc 96×96, số hướng, số frame và tốc độ animation chưa chốt. Cần thống nhất frame size, điểm neo, hướng và cách đặt tên; animation không khởi động lại mỗi frame. Chỉ flip trái/phải nếu thiết kế hình ảnh cho phép. Khi bổ sung asset, ghi nguồn và điều kiện sử dụng.

### Cấu trúc hiện tại và dự kiến

Hiện tại có `README.md`, `AGENTS.md` và **61 file Markdown trong `docs/phases/`** (ngoài metadata Git). Đây đều là tài liệu; chưa có code hoặc ứng dụng chạy được. Các thành phần triển khai dưới đây **chỉ là cấu trúc dự kiến**, chưa được tạo:

| Đường dẫn dự kiến | Nội dung |
| --- | --- |
| `game-client/src/` | scenes, entities, combat, skills, enemies, bosses, dungeon, ui, config; network khi đến nhóm E |
| `game-client/` — thư mục asset | Sprite, tilemap, hiệu ứng, âm thanh; chọn vị trí phục vụ asset khi cấu hình Vite |
| `game-server/` | room, player, game, combat, boss, network; auth và persistence thêm ở nhóm G |
| `docs/design/`, `docs/network/`, `docs/architecture/` và các thư mục tài liệu theo lĩnh vực | Đầu ra thiết kế/protocol/kiến trúc sẽ được viết khi thực hiện phase tương ứng; hiện chưa có |

## Roadmap tổng thể

**Tiến độ:** mới có tài liệu tổng hợp để review; Phase 0–3 chưa được coi là hoàn tất thiết kế, Phase 4–60 chưa triển khai. Có roadmap không đồng nghĩa với đã cho phép bắt đầu code.

Mỗi phase là một đơn vị giao việc, cần mục tiêu, phạm vi, phần loại trừ, ràng buộc kiến trúc, đầu ra, tiêu chí nghiệm thu và cách kiểm chứng. Thứ tự mặc định theo bảng; thay đổi phụ thuộc cần có lý do. Redis và scaling là các phase có điều kiện.

### Cách giao từng phase cho AI

Nhấn tên phase trong các bảng bên dưới để mở file riêng. Mỗi file có đầu vào/phụ thuộc, các bước cụ thể, phạm vi file dự kiến, phần không làm, checklist nghiệm thu, cách kiểm chứng, mẫu lệnh giao việc và chỗ ghi kết quả.

- **Review tài liệu:** yêu cầu “Chỉ rà soát/cập nhật tài liệu Phase N, chưa triển khai code”.
- **Thực hiện phase:** sao chép mục “Lệnh giao việc cho AI” trong file đã chọn. Phase 0–3 tạo đầu ra thiết kế; Phase 4 trở đi chỉ triển khai khi được giao.
- **Theo dõi kết quả:** cập nhật trạng thái và báo cáo ngay trong file phase, không đánh dấu xong chỉ vì đã có đặc tả. Tất cả phase hiện là `NOT_STARTED`.
- **Phụ thuộc:** mở liên kết phase cần có trước và kiểm tra đầu ra thật; không tự làm phase trước để bù phần còn thiếu. Một số việc như Redis/scaling/nội dung mới có thể `DEFERRED` khi chưa có nhu cầu.

Ví dụ mở đầu bằng [Phase 00 — Game Design Document](docs/phases/phase-00-game-design-document.md). Việc có 61 file giao việc không đồng nghĩa đã hoàn thành Phase 0–60.

### A — Thiết kế trước khi code

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 0 | [Game Design Document](docs/phases/phase-00-game-design-document.md) | Chốt concept, core loop, phạm vi MVP, nền tảng, cách thắng/thua và điểm còn mở |
| 1 | [Combat design](docs/phases/phase-01-combat-design.md) | Stat, công thức damage, trạng thái, hit timing và quy tắc cooldown đủ rõ để triển khai |
| 2 | [Class design](docs/phases/phase-02-class-design.md) | Vai trò và bộ skill tối thiểu của 4 class; chỉ rõ skill xử lý cơ chế nào |
| 3 | [Boss mechanic design](docs/phases/phase-03-boss-mechanic-design.md) | Thiết kế Golem, telegraph, shield/crystal/core, chuyển phase và tình huống thất bại |

### B — Vertical slice một người chơi

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 4 | [Client bootstrap](docs/phases/phase-04-client-bootstrap.md) | Client TypeScript/Vite/Phaser mở được trong browser với BootScene và GameScene |
| 5 | [Player movement](docs/phases/phase-05-player-movement.md) | Warrior placeholder di chuyển WASD, có hướng/state, giới hạn map và camera follow |
| 6 | [Player animation](docs/phases/phase-06-player-animation.md) | Idle/run chuyển đúng, không restart mỗi frame; thêm attack/hurt/death theo hành động |
| 7 | [Entity architecture](docs/phases/phase-07-entity-architecture.md) | Player và enemy dùng được thành phần chung, không dồn toàn bộ logic vào scene |
| 8 | [Skill system](docs/phases/phase-08-skill-system.md) | Skill definition, trạng thái thi triển và cooldown hoạt động độc lập với input |
| 9 | [Hitbox/hurtbox](docs/phases/phase-09-hitbox-hurtbox.md) | Hit được xác định bởi va chạm và thời điểm có hiệu lực |
| 10 | [Damage system](docs/phases/phase-10-damage-system.md) | Mọi thay đổi HP do tấn công đi qua pipeline chung, có sự kiện damage/death |
| 11 | [Enemy đầu tiên](docs/phases/phase-11-first-enemy.md) | Slime hoặc Skeleton phát hiện, đuổi, tấn công, nhận damage và chết |
| 12 | [Combat room](docs/phases/phase-12-combat-room.md) | Vào phòng, khóa cửa, sinh quái, dọn hết thì mở cửa |
| 13 | [Boss framework](docs/phases/phase-13-boss-framework.md) | State machine và pattern boss cơ bản dùng được |
| 14 | [Ancient Golem prototype](docs/phases/phase-14-golem-prototype.md) | Warrior có thể đánh boss solo, né telegraph, thắng hoặc thua |

**Gate vertical slice:** chơi xuyên suốt từ bắt đầu → đánh quái → mở cửa → boss → kết quả. Cần review cảm giác điều khiển và combat trước khi mở rộng.

### C — Bốn class và phối hợp

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 15 | [Character architecture](docs/phases/phase-15-character-architecture.md) | Thêm class qua cấu hình/thành phần mà không sao chép toàn bộ Warrior |
| 16 | [Tank](docs/phases/phase-16-tank.md) | Block, aggro/threat và taunt khiến boss đổi mục tiêu theo luật |
| 17 | [Mage](docs/phases/phase-17-mage.md) | Skill phép, projectile/AoE/status và khả năng xử lý rune shield |
| 18 | [Archer](docs/phases/phase-18-archer.md) | Bắn tầm xa, phát hiện hit ở bộ phận và xử lý weakpoint |
| 19 | [Warrior hoàn thiện](docs/phases/phase-19-warrior-finalization.md) | Combo/burst và tương tác rõ với trạng thái stagger |
| 20 | [Class synergy](docs/phases/phase-20-class-synergy.md) | Bốn entity cùng tham gia combat; mô phỏng offline bằng debug input/chuyển điều khiển hoặc AI đơn giản, kiểm chứng chu kỳ phối hợp |

Mô phỏng tại máy là cách thử thiết kế trước network, không tự mở rộng thành sản phẩm chơi solo hoặc hệ thống đồng đội AI đầy đủ.

### D — Dungeon hoàn chỉnh

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 21 | [Dungeon architecture](docs/phases/phase-21-dungeon-architecture.md) | Quản lý room, door, spawn, wave, checkpoint, boss room và trạng thái dungeon |
| 22 | [Enemy variety](docs/phases/phase-22-enemy-variety.md) | Quái giáp nặng, tầm xa/bay, bầy đàn hoặc charge tạo lợi thế cho từng class |
| 23 | [Mini boss](docs/phases/phase-23-mini-boss.md) | Một mini boss có hai cơ chế, ví dụ Shield Knight |
| 24 | [Full Golem](docs/phases/phase-24-full-golem.md) | Hoàn thiện shield, crystal, stagger, adds và enrage theo thiết kế đã chốt |
| 25 | [Dungeon MVP](docs/phases/phase-25-dungeon-mvp.md) | Một dungeon tĩnh chạy từ đầu đến kết quả, có phòng thường, mini boss và boss |

**Gate gameplay:** 4 class có quyết định riêng; telegraph và điểm yếu dễ hiểu; phối hợp tạo lợi thế thực tế. Chỉ đi tiếp network sau khi đã review mốc này trong phạm vi công việc được giao.

### E — Nền tảng multiplayer

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 26 | [Server bootstrap](docs/phases/phase-26-server-bootstrap.md) | Client kết nối WebSocket đến Spring Boot; chưa thêm DB |
| 27 | [Network protocol](docs/phases/phase-27-network-protocol.md) | Contract, version, payload, sequence, validation và lỗi được thống nhất |
| 28 | [Room system](docs/phases/phase-28-room-system.md) | Create/join/leave, chọn class, ready/start; bốn browser vào cùng room |
| 29 | [Player synchronization](docs/phases/phase-29-player-synchronization.md) | Các client thấy movement/direction/state của nhau với interpolation |
| 30 | [Network resilience](docs/phases/phase-30-network-resilience.md) | Heartbeat, phát hiện disconnect, sequence/timestamp và nền tảng reconnect |

Mốc này chứng minh kết nối và đồng bộ; chưa được coi là gameplay multiplayer hoàn chỉnh khi logic trận đấu chưa chuyển lên server.

### F — Server quyết định gameplay

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 31 | [Server game loop](docs/phases/phase-31-server-game-loop.md) | Vòng lặp nhận/kiểm tra lệnh, cập nhật mô phỏng và gửi snapshot/event; rõ quyền cập nhật room |
| 32 | [Authoritative movement](docs/phases/phase-32-authoritative-movement.md) | Server xác định vị trí từ input; client hiển thị prediction/reconciliation theo thiết kế |
| 33 | [Authoritative combat](docs/phases/phase-33-authoritative-combat.md) | Server kiểm tra skill, cooldown, state, range, hit và tính damage |
| 34 | [Server enemy AI](docs/phases/phase-34-server-enemy-ai.md) | Server quản lý mục tiêu, di chuyển, tấn công và chết của enemy |
| 35 | [Server boss](docs/phases/phase-35-server-boss.md) | Shield, weakpoint, aggro, phase, stagger và enrage thống nhất giữa các client |
| 36 | [Server dungeon](docs/phases/phase-36-server-dungeon.md) | Room clear, cửa, wave, boss, thắng/thua do server quyết định |

**Gate multiplayer:** 4 browser với 4 class cùng hoàn thành dungeon và thấy kết quả nhất quán; mất kết nối một người không làm server crash. Kiểm tra room isolation và yêu cầu không hợp lệ khi các chức năng tương ứng đã tồn tại.

### G — Tài khoản và progression

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 37 | [Authentication](docs/phases/phase-37-authentication.md) | Đăng nhập và phân quyền; lựa chọn JWT hoặc session theo thiết kế deployment |
| 38 | [PostgreSQL](docs/phases/phase-38-postgresql.md) | Schema và truy cập dữ liệu bền vững; không ghi trạng thái realtime từng tick |
| 39 | [Character persistence](docs/phases/phase-39-character-persistence.md) | Đăng nhập lại giữ class, level, EXP, skill và tiến trình theo thiết kế |
| 40 | [Loot system](docs/phases/phase-40-loot-system.md) | Server roll thưởng và ghi nhận có kiểm soát, không cấp trùng khi xử lý lại |
| 41 | [Inventory](docs/phases/phase-41-inventory.md) | Thêm/xóa/trang bị/tháo, bảo đảm tính nhất quán khi thao tác đồng thời |
| 42 | [Equipment](docs/phases/phase-42-equipment.md) | Slot trang bị và tác động stat rõ ràng, tránh làm hệ stat quá phức tạp |
| 43 | [Level/EXP](docs/phases/phase-43-level-exp.md) | Hoàn thành dungeon nhận EXP và tăng trưởng; gear không xóa vai trò cơ chế boss |
| 44 | [Difficulty](docs/phases/phase-44-difficulty.md) | Thay đổi pattern/cơ chế và nhịp đấu, không chỉ nhân HP |

### H — Hoàn thiện sản phẩm và mở rộng

| Phase | Nội dung | Đầu ra / tiêu chí hoàn thành |
| --- | --- | --- |
| 45 | [Matchmaking](docs/phases/phase-45-matchmaking.md) | Sau create/join room thủ công, bổ sung queue theo vai trò nếu cần |
| 46 | [Redis — có điều kiện](docs/phases/phase-46-redis.md) | Có nhu cầu cụ thể cho presence, room registry, queue, leaderboard hoặc cache |
| 47 | [Nhiều game server — có điều kiện](docs/phases/phase-47-multiple-game-servers.md) | Có bằng chứng cần scale; mỗi room được gắn với một instance sở hữu |
| 48 | [Reconnect hoàn chỉnh](docs/phases/phase-48-reconnect.md) | Grace period, khôi phục phiên và trạng thái; chốt cách xử lý hết thời gian chờ |
| 49 | [Anti-cheat hardening](docs/phases/phase-49-anti-cheat-hardening.md) | Bổ sung kiểm tra/log hành vi bất thường; validation nền tảng đã phải có ở E–F |
| 50 | [UI/UX](docs/phases/phase-50-ui-ux.md) | Lobby, HP, skill/cooldown, party, boss mechanic, kết quả và inventory rõ ràng |
| 51 | [VFX](docs/phases/phase-51-vfx.md) | Hiệu ứng hit, shield break, weakpoint, stagger và telegraph dễ phân biệt |
| 52 | [Audio](docs/phases/phase-52-audio.md) | Âm thanh hành động, cảnh báo boss và kết quả; phối hợp với tín hiệu thị giác |
| 53 | [Character art cuối](docs/phases/phase-53-final-character-art.md) | Thay placeholder bằng asset nhất quán cho 4 class và animation cần thiết |
| 54 | [Performance](docs/phases/phase-54-performance.md) | Đo client/server trước khi tối ưu; xử lý điểm nghẽn được quan sát |
| 55 | [Testing tổng thể](docs/phases/phase-55-testing.md) | Combat, room, persistence, mô phỏng và tải; tình huống trùng yêu cầu/disconnect/cleanup/restart |
| 56 | [Observability](docs/phases/phase-56-observability.md) | Log và metric cho room/player, tick time, latency, DB và lỗi |
| 57 | [Deployment](docs/phases/phase-57-deployment.md) | Quy trình build/deploy được kiểm chứng, client/API/WebSocket truy cập được |
| 58 | [Closed alpha](docs/phases/phase-58-closed-alpha.md) | Thu phản hồi về độ vui, độ rõ cơ chế, thời lượng và vai trò từng class |
| 59 | [Balance](docs/phases/phase-59-balance.md) | Điều chỉnh từ dữ liệu clear/death rate, skill usage và đóng góp từng vai trò |
| 60 | [Content expansion](docs/phases/phase-60-content-expansion.md) | Chỉ sau khi core ổn: dungeon/boss mới, skill, trang bị và các hệ mở rộng được chọn |

UI cơ bản, telegraph, validation và kiểm chứng phải có ngay khi gameplay cần. Các phase cuối là hoàn thiện và kiểm tra tổng thể, không phải lý do trì hoãn chất lượng đến cuối dự án.

### Các milestone để review

| Milestone | Phase | Bằng chứng cần có |
| --- | --- | --- |
| M0 — Design | 0–3 | Luật chơi và phạm vi đủ rõ; các quyết định ảnh hưởng prototype được xử lý |
| M1 — Combat prototype | 4–11 | Warrior và enemy đánh nhau hoàn chỉnh |
| M2 — Vertical slice | 12–14 | Phòng chiến đấu và boss solo có thắng/thua |
| M3 — Four heroes | 15–20 | Bốn class và phối hợp hoạt động trong mô phỏng offline |
| M4 — Dungeon MVP | 21–25 | Dungeon offline hoàn chỉnh, gameplay đủ tốt để chuyển sang network |
| M5 — Network foundation | 26–30 | Bốn browser cùng room, đồng bộ và xử lý kết nối cơ bản |
| M6 — Multiplayer MVP | 31–36 | Server quyết định trận đấu; bốn người hoàn thành dungeon |
| M7 — Progression | 37–44 | Tài khoản, nhân vật, loot/inventory và tăng trưởng bền vững |
| M8 — Production/mở rộng | 45–60 | Các hạng mục được chọn đạt tiêu chí; scaling và content không tự động là điều kiện phát hành |

## Quyết định còn mở

| Chủ đề | Cần chốt trước khi nào |
| --- | --- |
| Tên game, góc nhìn, desktop/mobile, bàn phím/chuột hay cảm ứng | Phase 0; top-down và desktop là đề xuất ban đầu |
| Mỗi đội bắt buộc đủ một người mỗi class, xử lý trùng class/thiếu người, chết/revive/team wipe | Thiết kế ở Phase 0–3, hiện thực theo phase liên quan |
| Số skill/passive, mana/tài nguyên, cooldown, damage, targeting, friendly fire, va chạm đồng đội | Phase 1–2 |
| Rune/crystal có bắt buộc đúng class, thứ tự cơ chế, reset và timeout, điều kiện thắng/thua | Phase 3 |
| Thời lượng dungeon, số wave/quái, checkpoint và cách chơi lại | Phase 0 và thiết kế chi tiết trước Phase 21–25 |
| Style, frame size, hướng nhìn và nguồn asset | Placeholder trước Phase 6; art hoàn chỉnh ở Phase 53 |
| Phiên bản stack, package manager và Maven/Gradle | Trước bootstrap client/server tương ứng |
| Protocol, mô hình thread/tick, reconnect, giới hạn room và mục tiêu latency | Thiết kế trước Phase 27–31 |
| JWT/session, phân phối loot cá nhân/chung, schema, slot trang bị và cách tăng level | Trước các phase nhóm G tương ứng |
| Ngân sách vận hành, nơi deploy và nhu cầu Redis/multi-instance | Trước các phase nhóm H tương ứng |

Trong giai đoạn hiện tại, bước tiếp theo phù hợp là review Phase 0–3 bằng tài liệu. Chỉ bắt đầu triển khai khi người dùng giao công việc có code; khi đó tuân theo [AGENTS.md](AGENTS.md) và phạm vi phase được giao.
