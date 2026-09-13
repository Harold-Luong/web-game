# Game Design Document — web-game

| Thuộc tính | Giá trị |
| --- | --- |
| Phiên bản tài liệu | 0.1 |
| Phạm vi | Đầu ra thiết kế sản phẩm của Phase 00 |
| Trạng thái | Bản thiết kế để review; các đề xuất được đánh dấu riêng |
| Hiện trạng sản phẩm | Chưa có code, asset game hoặc phiên chơi để kiểm chứng |
| Tài liệu liên quan | [README](../../README.md), [AGENTS](../../AGENTS.md), [đặc tả Phase 00](../phases/phase-00-game-design-document.md) |

## 1. Mục đích và nguồn quyết định

GDD xác định trải nghiệm cần xây, vòng chơi, phạm vi từng mốc và các tình huống kết thúc. Tài liệu này là đầu vào cho thiết kế combat, class và boss; chưa thay thế các đặc tả chi tiết đó.

Nguồn yêu cầu là cuộc trò chuyện đã được tổng hợp trong [README — Nguồn và cách đọc](../../README.md#nguồn-và-cách-đọc), yêu cầu hiện tại thực hiện Phase 00 bằng tài liệu, và hai lựa chọn người dùng đã trả lời trong lượt này: top-down trên máy tính với bàn phím/chuột; gục và cứu đồng đội, cả đội gục thì thua. Không suy ra việc người dùng duyệt một gợi ý chỉ vì gợi ý từng xuất hiện trong cuộc trò chuyện.

Quy ước:

- **Đã xác nhận:** yêu cầu do người dùng nêu rõ.
- **Đề xuất v0.1:** lựa chọn làm cơ sở cụ thể để review và walkthrough. Chưa phải quyết định đã được người dùng xác nhận; thay đổi phải được phản ánh vào thiết kế phụ thuộc.
- **Chưa chốt:** nội dung cần quyết định ở phase được chỉ rõ; chưa dùng để tự triển khai phần phụ thuộc.

Các luồng có nhãn đề xuất bên dưới được đọc theo bộ lựa chọn v0.1 nhất quán. Hoàn thành tài liệu không đồng nghĩa mọi đề xuất đã được duyệt hoặc gameplay đã được chứng minh là vui.

## 2. Concept và trải nghiệm cốt lõi

**Đã xác nhận:** game web 2D co-op, đội 4 người sử dụng Tank, Mage, Archer và Warrior để vượt ải. Boss có điểm yếu/cơ chế khiến từng vai trò phát huy sức mạnh và cần phối hợp.

Mỗi trận cần tạo cảm giác cả đội cùng tạo ra cơ hội chiến thắng: Tank điều khiển tình thế, Mage giải quyết cơ chế phép, Archer đánh đúng mục tiêu, Warrior tận dụng sơ hở. Người chơi hiểu hành động của mình đã giúp đồng đội như thế nào.

**Đề xuất v0.1:** dungeon fantasy có phòng chiến đấu và boss, dành cho nhóm bạn chơi từng phiên ngắn. Có thể tham gia lại nhiều lượt để cải thiện phối hợp. `web-game` là tên repository; Dungeon Bonds chỉ là tên sản phẩm tham khảo. Cốt truyện dài và tên thương mại không phải điều kiện để bắt đầu prototype.

### Trụ cột thiết kế

| Trụ cột | Biểu hiện cần quan sát khi có bản chơi |
| --- | --- |
| Bốn vai trò có giá trị | Mỗi class có quyết định và đóng góp riêng ngoài tổng damage |
| Cơ chế dễ đọc | Người chơi nhận biết đòn nguy hiểm, mục tiêu cơ chế và thời gian tấn công thuận lợi |
| Phối hợp tạo cơ hội | Hành động của một vai trò giúp vai trò khác thực hiện nhiệm vụ |
| Lượt chơi có kết thúc rõ | Đội hiểu vì sao thắng/thua và có thể bắt đầu lại mà không bị kẹt |
| Phạm vi đủ nhỏ để kiểm chứng | Một dungeon và một boss chính trước khi mở rộng nội dung hoặc progression |

Không dùng tổng DPS làm thước đo duy nhất: một lần Tank xoay đúng hướng boss hoặc Mage phá rune có thể quan trọng hơn lượng damage trực tiếp.

## 3. Nền tảng, góc nhìn và điều khiển

**Đã xác nhận trong Phase 00:** browser trên máy tính, góc nhìn top-down 2D, bàn phím và chuột. Phím cụ thể, cách ngắm và danh sách browser kiểm thử trong bảng dưới vẫn là đề xuất cần thiết kế tiếp.

| Thành phần | Đề xuất v0.1 | Cần xác định thêm |
| --- | --- | --- |
| Thiết bị | Đã xác nhận máy tính có bàn phím và chuột | Danh sách browser và kích thước màn hình kiểm thử trước Phase 04 |
| Góc nhìn | Đã xác nhận top-down; đề xuất camera theo nhân vật | Số hướng sprite và cách ngắm trong Phase 01/06 |
| Di chuyển | WASD; nhả phím thì dừng; tốc độ chéo không cao hơn đi thẳng | Tốc độ và tương tác va chạm trong thiết kế combat |
| Đánh thường | Chuột trái, hướng ngắm theo vị trí chuột | Giữ hay nhấn từng lần, vùng đánh và target ở Phase 01 |
| Hai skill MVP | Q và E | Skill nào gắn phím nào ở Phase 02 |
| Tương tác/cứu đồng đội | F | Giữ phím, phạm vi, thời gian và điều kiện ngắt ở Phase 01 |
| Menu | Escape mở menu/cài đặt | Trong multiplayer, mở menu không tạm dừng trận của cả đội |

Space/dash không phải một năng lực mặc định cho mọi class; dash/leap chỉ có nếu nằm trong bộ skill đã chọn. Giao diện cảm ứng, gamepad và hỗ trợ mobile thuộc phần chưa chọn cho MVP v0.1. Không khóa kích thước sprite, tốc độ animation hoặc phiên bản engine ở Phase 00.

## 4. Bốn class và trách nhiệm trong đội

**Đã xác nhận:** cần đủ bốn vai trò trong concept. **Đề xuất v0.1:** mỗi người giữ một class trong suốt lượt dungeon; cấu hình kỹ năng MVP là đánh thường + hai skill. Passive và skill mở rộng để Phase 02 quyết định, chưa tự bổ sung vào phạm vi.

| Class | Việc người chơi thường làm | Đóng góp trong cơ chế boss | Dấu hiệu thiết kế thất bại cần tránh |
| --- | --- | --- | --- |
| Tank — Đỡ đòn | Chọn vị trí, giữ hướng đối thủ, bảo vệ khoảng trống | Quản lý aggro, đỡ hoặc hướng đòn nguy hiểm ra khỏi đội | Chỉ đứng chịu damage và chờ người khác chơi |
| Mage — Pháp sư | Chọn vùng tác động, kiểm soát nhóm quái | Phá rune/khiên phép và xử lý cơ chế phép | Chỉ spam AoE, không có nhiệm vụ riêng |
| Archer — Cung thủ | Giữ khoảng cách, ngắm mục tiêu ưu tiên | Bắn crystal/bộ phận/điểm yếu cần độ chính xác | Đánh body liên tục cũng cho kết quả như ngắm đúng |
| Warrior — Chiến binh | Áp sát đúng lúc, chọn thời điểm dồn sát thương | Đánh lõi hoặc mục tiêu khi bị stagger/lộ sơ hở | Đứng chém liên tục hiệu quả như phối hợp mở burst window |

GDD chưa quy định stat, multiplier, cooldown hoặc danh sách skill cụ thể. Phase 02 phải chứng minh bộ tối thiểu của mỗi class đủ làm nhiệm vụ, không buộc triển khai mọi tên skill tham khảo trong README.

## 5. Vòng chơi và các màn hình chính

**Đề xuất v0.1 cho multiplayer MVP:**

1. Mở game và vào màn hình bắt đầu. Giai đoạn chưa có tài khoản dùng danh tính phiên tạm; login chỉ xuất hiện khi triển khai nhóm G.
2. Tạo phòng hoặc nhập mã phòng để tham gia nhóm bạn.
3. Chọn class, xem vai trò còn thiếu và xác nhận sẵn sàng.
4. Khi đủ điều kiện, bắt đầu lượt dungeon và chờ cả đội tải xong nội dung cần thiết.
5. Vượt phòng quái, mini boss, phòng nghỉ và boss chính.
6. Nhận màn hình thắng/thua cùng lý do và lựa chọn chơi lại hoặc về lobby.
7. Trở về lobby, giữ nhóm nếu còn đủ thành viên, chọn lại/sẵn sàng cho lượt mới.

Khi tới progression, bổ sung bước nhận loot/EXP đã được server ghi nhận, quản lý trang bị và chọn thử thách khó hơn. Multiplayer MVP không cần inventory hoặc phần thưởng bền vững để được xem là chơi hoàn chỉnh.

| Màn hình/trạng thái | Thông tin và thao tác cần có |
| --- | --- |
| Bắt đầu | Chơi/tạo/tham gia phòng theo mốc triển khai, hướng dẫn input ngắn |
| Lobby | Thành viên, class, ready, mã phòng, điều kiện còn thiếu, rời phòng |
| Loading | Tiến trình sẵn sàng của phiên, lỗi tải và cách quay lại lobby |
| Trong dungeon | HP bản thân/đội, người gục hoặc mất kết nối, skill/cooldown, HP boss, tín hiệu cơ chế |
| Kết quả | Thắng/thua, lý do, thời lượng nếu có, chơi lại/về lobby |
| Mất kết nối | Đang kết nối lại, slot còn được giữ hay đã hết thời gian, kết quả phục hồi |

HUD cơ bản và tín hiệu mechanic phải có khi gameplay cần, dù UI hoàn thiện còn nằm ở Phase 50.

## 6. Luật phòng và đội hình — đề xuất v0.1

| Tình huống | Kết quả đề xuất |
| --- | --- |
| Tạo phòng | Có một người tạo phòng điều khiển bắt đầu; tối đa bốn slot người chơi |
| Chọn class | Mỗi class tối đa một slot; giao diện nêu rõ class đã có người chọn |
| Chỉ có ba người hoặc thiếu một class | Không được bắt đầu; hiển thị vai trò còn thiếu |
| Đủ bốn người, bốn class, tất cả ready | Người tạo phòng có thể bắt đầu; hệ thống kiểm tra lại điều kiện tại lúc start |
| Đổi class hoặc thành viên vào/rời khi ở lobby | Hủy trạng thái ready để đội xác nhận lại đội hình mới |
| Hai người đồng thời chọn cùng class | Chỉ một lựa chọn được chấp nhận; người còn lại nhận trạng thái phòng mới nhất |
| Người tạo phòng rời lobby | Chuyển quyền bắt đầu cho người còn lại vào phòng sớm nhất; phòng trống thì đóng |
| Dungeon đã bắt đầu | Khóa class và đội hình; không cho người mới thay một vai trò giữa trận |
| Rời phòng khi đang chơi | Được báo ảnh hưởng tới đội; mất vai trò được xử lý theo mục 9 |

Không tự thêm matchmaking, bot lấp slot, spectator hoặc hỗ trợ nhóm 2–3 người vào bản đầu. Mô phỏng offline bốn class là công cụ phát triển; không phải ngoại lệ của luật đội hình sản phẩm multiplayer.

## 7. Cấu trúc dungeon và boss

**Đề xuất v0.1:** một dungeon tĩnh, tạm dùng Ancient Golem làm boss chính. Thời lượng giả thuyết 10–20 phút cho lượt hoàn thành; đây là mục tiêu chơi thử, không phải timeout khiến đội tự thua.

| Chặng | Mục đích | Điều kiện đi tiếp |
| --- | --- | --- |
| Phòng bắt đầu | Kiểm tra input/HUD và tập hợp đội | Cả đội sẵn sàng bước vào encounter đầu |
| Phòng chiến đấu 1 | Học nhịp đánh/né cơ bản | Dọn hết enemy bắt buộc của phòng |
| Phòng chiến đấu 2 | Phối hợp chọn mục tiêu và xử lý vai trò quái | Hoàn thành wave/cơ chế bắt buộc |
| Mini boss | Tập phối hợp qua hai cơ chế đơn giản | Hạ mini boss và encounter kết thúc |
| Phòng nghỉ | Tập hợp, cứu người còn gục trước boss | Đội chủ động mở encounter kế tiếp khi đủ điều kiện |
| Boss chính | Kiểm chứng vai trò cả bốn class | Hạ boss theo luật kết thúc |
| Kết quả | Hiểu kết quả và bắt đầu lượt tiếp theo | Chơi lại hoặc quay về lobby |

Khi encounter bắt đầu, cửa liên quan khóa; cửa mở sau khi đạt điều kiện clear. **Đề xuất:** chuyển sang encounter tiếp theo khi cả bốn nhân vật đã có mặt và có thể hành động, tránh bỏ người gục ở phòng trước. Phòng nghỉ chưa có cửa hàng, nâng cấp giữa lượt hoặc buff ngẫu nhiên. Hồi HP tự động tại phòng nghỉ vẫn chưa chốt; walkthrough không giả định có hồi HP miễn phí.

Quái nên gợi các quyết định khác nhau: quái giáp nặng, bầy đàn, mục tiêu xa và đòn charge. Số loại, số quái và số wave chi tiết thuộc nhóm D; không khóa các con số đó trong GDD.

### Nhịp phối hợp boss ở mức concept

Tank giữ vị trí/hướng boss → Mage xử lý rune shield → Archer phá crystal → mở thời gian stagger/lộ lõi → Warrior dồn sát thương; đội lặp lại và xử lý các thay đổi nhịp đánh.

Đây là chu kỳ minh họa, chưa chốt thành một state machine tuyến tính bắt buộc. Phase 03 phải chọn điều kiện vào/ra, class nào được tác động, việc xử lý sai và cách reset. Ở mức sản phẩm, một lần hụt cơ chế cần có kết quả rõ: đóng cửa sổ tấn công, lặp cơ chế hoặc thất bại đã báo trước; không để đội ở trạng thái không còn hành động nào có thể tiến triển.

Prototype Warrior solo dùng boss giản lược, có thể hoàn thành mà không cần kỹ năng Tank/Mage/Archer. Bản team mới kiểm chứng đầy đủ bốn vai trò.

## 8. Hết HP, cứu đồng đội, thắng/thua và chơi lại

**Đã xác nhận trong Phase 00:** hết HP thì gục, đồng đội có thể cứu; cả đội gục thì thua. GDD quy định kết quả ở cấp vòng chơi. Hạn chế hành động lúc gục, cách cứu, thời gian/phạm vi/HP hồi và trường hợp kết quả đồng thời bên dưới vẫn là đề xuất hoặc chi tiết thuộc Phase 01.

### Luật trạng thái người chơi

| Trạng thái | Hành vi đề xuất |
| --- | --- |
| Đang chiến đấu | Có thể di chuyển, tấn công, dùng skill và tương tác theo luật combat |
| Gục khi HP về 0 | Không di chuyển/tấn công/dùng skill; có tín hiệu để đồng đội nhận biết và đến cứu |
| Được cứu | Trở lại hành động với lượng HP theo thiết kế combat; không đổi class hoặc reset boss |
| Cả đội gục | Kết thúc encounter/lượt dưới dạng thất bại; không tự hồi sinh đồng loạt ngay giữa combat |

Đề xuất cho bản đầu: người gục chờ được cứu, chưa thêm đồng hồ mất máu dẫn tới chết vĩnh viễn. Một người còn hành động được có thể cứu lần lượt đồng đội. Cứu cần tương tác chủ động và có thể bị ngắt; cách ngắt, khoảng cách, thời gian, số lần cứu và HP hồi phải được xác định ở Phase 01 trước khi triển khai. Nếu không có khả năng tiếp tục, đội có đường kết thúc lượt/quay về lobby, không phải chờ vô hạn.

**Ngoại lệ prototype solo:** Warrior hết HP thì thua ngay vì chưa có đồng đội. Mô phỏng team ở nhóm C–D mới kiểm chứng cứu người; không kéo hệ thống revive đầy đủ vào Phase 11.

### Luật kết quả lượt chơi

| Sự kiện | Kết quả đề xuất |
| --- | --- |
| Boss chính bị hạ và hệ thống ghi nhận clear | Thắng; chốt kết quả một lần, ngừng encounter và mở màn hình kết quả |
| Cả đội gục trước khi đạt clear | Thua vì team wipe |
| Một người gục nhưng còn người cứu | Trận tiếp tục; không tự thua chỉ vì mất tạm một vai trò |
| Bỏ lỡ một burst window | Tiếp tục chu kỳ boss theo Phase 03; không tự tính là thua toàn dungeon |
| Người chơi rời hẳn hoặc hết thời gian giữ slot | Kết thúc lượt vì đội không còn đủ vai trò, theo mục 9 |
| Cả đội không tải vào trận được | Hủy bắt đầu, về lobby với lý do tải/kết nối; không coi là thắng/thua combat |
| Boss chết và người chơi cuối gục trong cùng bước xử lý | Đề xuất ưu tiên clear nếu boss death hợp lệ đã được xử lý trong bước đó; chỉ tạo một kết quả |

Quy tắc ưu tiên clear/team wipe là đề xuất sản phẩm cần Phase 01/03 cụ thể hóa, không phải claim về vòng lặp server hiện có. Sau khi kết quả đã chốt, event muộn không đổi thắng thành thua hoặc phát kết quả thứ hai. Ở multiplayer, server là nơi quyết định kết quả cuối cùng.

### Retry và tiến trình trong lượt

**Đề xuất v0.1:** thua hoặc thắng xong đều quay về lobby để cả đội ready lại; lượt mới bắt đầu từ đầu dungeon. Giữ nhóm/class nếu thành viên không đổi, nhưng reset ready, HP, cooldown và state encounter theo cấu hình lượt mới.

Chưa cam kết checkpoint retry từ giữa dungeon. Checkpoint xuất hiện trong roadmap Phase 21 là khả năng thiết kế cần review, không tự đưa vào MVP. Nút retry trực tiếp trong prototype solo có thể khởi động lại vertical slice từ đầu.

Multiplayer MVP chưa lưu lượt đang dở qua reload/server restart và chưa có phần thưởng bền vững. Khi tới nhóm G, loot/EXP chỉ thêm theo luật progression riêng; thất bại không tự trừ trang bị hay vật phẩm đã sở hữu nếu chưa có thiết kế cho điều đó.

## 9. Thiếu vai trò và gián đoạn kết nối

**Đề xuất v0.1:**

- **Trước trận:** thiếu người hoặc class thì ở lobby; không bù bằng bot hay tự chuyển sang chế độ ít người.
- **Gục trong trận:** ưu tiên cứu đồng đội để khôi phục vai trò. Cơ chế boss phải có nhịp lặp/thời gian phục hồi, hoặc điều kiện fail được mô tả ở Phase 03.
- **Mất mạng tạm thời:** giữ định danh/slot trong một khoảng chờ có giới hạn, báo cả đội và cho đúng người trở lại. Chưa chốt số giây; Phase 30/48 sẽ xác định theo nhu cầu thử mạng.
- **Trong khoảng chờ:** trận tiếp tục, người mất mạng không nhận input mới; không tự cấp bất tử, damage hoặc điều khiển bằng bot. Hành vi nhân vật còn ở mô phỏng và khả năng nhận damage cần được Phase 30/33/48 thiết kế nhất quán; không dùng thời gian chờ làm cơ chế né đòn miễn phí.
- **Không còn người kết nối có thể hành động nhưng vẫn có phiên chờ quay lại:** chỉ chờ đến giới hạn đã định nếu chưa xảy ra team wipe; hết giới hạn thì kết thúc vì thiếu đội hình. Nếu toàn bộ nhân vật đã gục thì áp dụng team wipe.
- **Hết khoảng chờ hoặc rời hẳn:** kết thúc lượt với lý do thiếu vai trò và trở lại lobby; không cho người mới thay thế giữa trận trong MVP này.
- **Quay lại sau khi lượt đã kết thúc:** hiển thị kết quả hoặc đưa về lobby, không khôi phục nhân vật trong encounter đã bị dọn.
- **Server mất state trận sau restart:** báo lượt không thể phục hồi và về lobby. Chỉ hứa phục hồi nếu một phase sau đã thiết kế, triển khai và kiểm chứng khả năng đó.

Đây là luật trải nghiệm dự kiến; không thiết kế reconnect token, network message hoặc kiến trúc phục hồi trong Phase 00. Nếu thay chính sách cho phép đội thiếu người tiếp tục, phải review lại toàn bộ cơ chế bắt buộc class ở Phase 03.

## 10. Phạm vi và điều kiện đạt từng mốc

Các mốc dưới đây là ranh giới phạm vi v0.1 để giao việc, chưa phải tính năng đã có. Giữ hệ số phase 0–60 như README.

| Mốc | Phải có | Chưa nằm trong phạm vi | Bằng chứng cần có sau triển khai |
| --- | --- | --- | --- |
| M0 — Thiết kế, Phase 00–03 | GDD, combat, class và boss design đủ nhất quán | Code hoặc gameplay đã kiểm chứng | Walkthrough thiết kế; câu hỏi ảnh hưởng triển khai được xử lý ở đúng phase |
| M1–M2 — Vertical slice, Phase 04–14 | Một Warrior, movement, animation placeholder, combat, một loại quái, combat room, Golem solo, thắng/thua/retry | Lobby, 4 class, revive team, backend, inventory | Chơi từ đầu tới thắng và thua; điều khiển/telegraph hoạt động |
| M3–M4 — Dungeon offline, Phase 15–25 | Đủ 4 class trong mô phỏng tại máy, phối hợp, một dungeon tĩnh, mini boss/Golem team, luật gục/cứu đã được chọn | Multiplayer thật, tài khoản, DB, progression | Chu kỳ bốn vai trò hoàn thành được; dungeon không kẹt khi retry hoặc hụt mechanic |
| M5 — Nền tảng network, Phase 26–30 | Bốn client vào phòng, đội hình/ready, đồng bộ movement và xử lý kết nối cơ bản | Gameplay authoritative hoàn chỉnh, persistence | Bốn browser thấy nhau; join/leave và room isolation được kiểm tra |
| M6 — Multiplayer MVP, Phase 31–36 | Server quản lý movement, combat, AI, boss, dungeon và kết quả; bốn người chơi toàn lượt | Loot/EXP bền vững, equipment, auto matchmaking, scaling | Bốn người thắng/thua/retry nhất quán; disconnect không làm server crash |
| M7 — Progression, Phase 37–44 | Auth, nhân vật, loot, inventory, equipment, EXP/level và difficulty được chọn | Trading, auction, crafting phức tạp, talent mở rộng | Dữ liệu còn sau login/restart; không cấp trùng reward; cơ chế boss vẫn có giá trị |
| M8 — Production, Phase 45–60 theo nhu cầu | Các phần polish, quality và vận hành được chọn | Không mặc định tất cả hạng mục là điều kiện phát hành | Playtest và kiểm chứng vận hành; Redis/scaling/content chỉ khi có nhu cầu |

Yêu cầu gục/cứu đã được người dùng chọn trong Phase 00: cần đặc tả tại Phase 01, mô phỏng tại Phase 20 và đồng bộ authoritative tại Phase 33–36. Đây không phải cho phép bắt đầu các phase đó trong nhiệm vụ hiện tại.

### Ngoài MVP v0.1

PvP; guild; open world; trading/auction; crafting phức tạp; dungeon procedural lớn; nhiều dungeon/boss chính; class mới; talent tree; seasonal content; voice chat; shop tiền thật. Mobile/gamepad, matchmaking tự động, bot chơi thay và checkpoint retry giữa dungeon chưa được chọn cho bản đầu. Không dùng các hạng mục đó để trì hoãn việc kiểm chứng một dungeon nhỏ.

## 11. Định hướng hình ảnh, phản hồi và âm thanh

**Đề xuất:** fantasy cartoon/pixel-ish, silhouette và hiệu ứng của bốn class dễ phân biệt. Prototype dùng placeholder; concept nhân vật từ cuộc trò chuyện chưa có dưới dạng asset trong repository.

Ưu tiên thể hiện trạng thái có ích: hướng boss, vùng sắp gây damage, shield/rune còn hoạt động, crystal có thể đánh, stagger/core window, người cần cứu. Tín hiệu không chỉ dựa vào màu hoặc âm thanh; phối hợp hình dạng, vị trí, chuyển động và nhãn khi cần.

Frame size, số hướng, số frame, âm thanh và nguồn asset sẽ được chọn theo phase liên quan. Phase 00 không tạo art, sprite sheet, âm thanh hoặc mã animation.

## 12. Câu hỏi chơi thử và thước đo

Chưa có số liệu thực. Các nội dung này là kế hoạch quan sát khi đến gate gameplay, không phải cam kết FPS, latency hoặc kết quả balance.

| Câu hỏi | Cách kiểm chứng dự kiến |
| --- | --- |
| Người chơi có hiểu vì sao vừa trúng đòn? | Quan sát lượt né telegraph và hỏi lại sau encounter |
| Mỗi class có quyết định riêng? | Ghi hành động aggro/block, rune, weakpoint và burst, không chỉ damage |
| Phối hợp có tạo lợi thế? | So lượt làm đúng chu kỳ với lượt bỏ lỡ một vai trò trong cùng điều kiện |
| Có ai phải chờ quá lâu? | Ghi thời gian gục, thời gian không có mục tiêu phù hợp và thời gian tìm đủ đội |
| Dungeon có quá dài? | Đo thời lượng lượt thắng/thua, số lần retry và vị trí người thử muốn dừng |
| Quy tắc cứu/retry có phù hợp? | Quan sát một người gục và team wipe; ghi cảm giác mất tiến trình khi phải chơi lại từ đầu |

GDD chỉ đề xuất thời lượng 10–20 phút. Mốc M2/M4 cần chơi thử trước khi kết luận gameplay đạt; trạng thái DONE của tài liệu Phase 00 không đánh dấu các gate đó đã qua.

## 13. Sổ quyết định và điểm cần review

| ID | Chủ đề | Trạng thái / lựa chọn hiện tại | Nơi cần xử lý tiếp |
| --- | --- | --- | --- |
| C-01 | Sản phẩm | Đã xác nhận: web game 2D co-op vượt ải | Giữ xuyên suốt roadmap |
| C-02 | Vai trò | Đã xác nhận: 4 người, Tank/Mage/Archer/Warrior, boss có điểm yếu để phối hợp | Phase 01–03 cụ thể hóa |
| C-03 | Phạm vi lượt hiện tại | Đã xác nhận: chỉ thực hiện Phase 00 bằng tài liệu | Không tạo code hoặc tự làm Phase 01 |
| C-04 | Thiết bị và góc nhìn | Đã xác nhận trong lượt Phase 00: máy tính, top-down, bàn phím/chuột | Phase 01 chọn targeting/input cụ thể; Phase 04 chọn browser kiểm thử |
| P-02 | Luật đội hình | Đề xuất: đúng một người mỗi class, đủ 4 người và ready mới start, khóa class trong lượt | Review trước Phase 03/28 |
| C-05 | Hết HP trong đội | Đã xác nhận trong lượt Phase 00: gục, đồng đội cứu; cả đội gục thì thua | Phase 01 thiết kế chi tiết revive; solo thua ngay vẫn là ngoại lệ prototype được đề xuất |
| P-04 | Retry/checkpoint | Đề xuất: team về lobby rồi chơi lại từ đầu; chưa retry giữa dungeon | Review trước Phase 21; giữ câu hỏi chi phí chơi lại cho playtest |
| P-05 | Skill MVP | Đề xuất: basic + 2 skill, chưa mặc định passive | Phase 02 chọn skill bảo đảm xử lý cơ chế |
| P-06 | Nội dung/thời lượng | Đề xuất: một dungeon tĩnh, mini boss, Ancient Golem; mục tiêu thử 10–20 phút | Phase 03 và 21–25 |
| P-07 | Cùng lúc thắng/thua | Đề xuất ưu tiên clear hợp lệ trong cùng bước xử lý; kết quả chỉ chốt một lần | Phase 01/03 định nghĩa nhất quán |
| P-08 | Disconnect | Đề xuất giữ slot có giới hạn; hết chờ/rời hẳn thì kết thúc lượt vì thiếu đội hình | Phase 30/48 định nghĩa timeout và hành vi chi tiết |
| O-01 | Công thức combat | Chưa chốt: damage, stat, cooldown, resource, friendly fire, va chạm đồng đội, targeting | Phase 01; ảnh hưởng Phase 08–10 |
| O-02 | Chi tiết cứu người | Chưa chốt: thời gian, range, ngắt, HP hồi, giới hạn cứu; đề xuất chưa có bleed-out | Phase 01 dựa trên yêu cầu C-05 |
| O-03 | Luật điểm yếu boss | Chưa chốt: bắt buộc class hay lợi thế, thứ tự shield/crystal, reset, fail mechanic | Phase 03 |
| O-04 | Phòng nghỉ | Chưa chốt hồi HP tự động; v0.1 chỉ dùng để tập hợp/cứu người | Phase 01/21 trước khi triển khai hồi phục |
| O-05 | Nhận diện sản phẩm | Tên game, art cuối và asset chưa chốt | Không chặn thiết kế combat; quyết định trước khi làm art cuối |
| O-06 | Progression và hạ tầng | Chưa chốt loot cá nhân/chung, EXP curve, auth, phiên bản stack và deployment | Các phase tương ứng, không giải quyết thay trong Phase 00 |

C-04/C-05 được ghi nhận từ câu trả lời trực tiếp của người dùng trong lượt Phase 00. Các dòng P còn lại vẫn là đề xuất; các dòng O là chi tiết chưa chốt. Nếu lựa chọn thay đổi, cập nhật walkthrough và ranh giới scope trước khi triển khai phần chịu ảnh hưởng.

## 14. Walkthrough kiểm chứng trên giấy

Đây là kiểm tra logic tài liệu theo bộ đề xuất v0.1, chưa phải test trong game. Kết quả chỉ chứng minh đường đi đã được mô tả và các chỗ thiếu đã được chỉ rõ.

| ID | Kịch bản | Đường đi và kết quả dự kiến | Đối chiếu |
| --- | --- | --- | --- |
| W-01 | Lượt thắng của đội đủ class | 4 người chọn 4 class → tất cả ready → vào dungeon → clear hai phòng → mini boss → tập hợp phòng nghỉ → hoàn thành chu kỳ Golem → boss chết → kết quả thắng → lobby | Mục 5–8; không đòi loot/inventory trước nhóm G |
| W-02 | Team wipe ở Golem | Đội vào boss → một người gục → người còn lại có thể cứu → nếu cả bốn gục trước clear thì chốt thua → lobby → ready lại và dungeon mới từ đầu | Mục 8; state cũ không đi sang lượt mới |
| W-03 | Thiếu Archer trước trận | Ba người chọn Tank/Mage/Warrior → start bị chặn và hiện thiếu Archer → người thứ tư chọn Archer → cả đội ready lại → bắt đầu được | Mục 6; không âm thầm thêm bot |
| W-04 | Trùng class | Hai người chọn Mage → một người được giữ lựa chọn → người còn lại chọn vai trò còn thiếu → mọi người ready lại | Mục 6; cần server xử lý tranh chấp khi đến network |
| W-05 | Mage gục giữa cơ chế rune | Mage không thể phá rune → một người còn hành động đến cứu → Mage trở lại → đội tiếp tục chu kỳ phù hợp | Mục 8; thời gian cứu thuộc O-02, cửa sổ/reset boss thuộc O-03, chưa tự coi các con số đã có |
| W-06 | Mất mạng rồi quay lại | Giữ slot trong khoảng chờ → đúng người kết nối lại → nếu lượt còn hoạt động thì trở lại state hiện tại, không tạo nhân vật mới | Mục 9; thời gian chờ và restore chi tiết ở Phase 30/48 |
| W-07 | Mất người hẳn | Một vai trò rời hẳn hoặc hết thời gian giữ slot → lượt kết thúc vì thiếu đội hình → lobby đợi đủ vai trò | Mục 9; không chờ mechanic bất khả thi vô hạn |
| W-08 | Prototype solo thua | Warrior vào vertical slice → HP về 0 → defeat → retry từ đầu | Mục 8 và 10; không yêu cầu hệ revive/team trước nhóm C |
| W-09 | Boss và người cuối cùng cùng hết HP | Clear hợp lệ được ghi nhận trong bước xử lý → ưu tiên thắng theo P-07 → không phát thêm defeat | Mục 8; cần Phase 01/03 chốt chi tiết thứ tự |
| W-10 | Server restart giữa lượt | Phiên mất state → báo không thể phục hồi lượt → về lobby khi dịch vụ trở lại | Mục 9; không hứa tiếp tục trận chưa được hỗ trợ |

### Đối chiếu acceptance criteria của Phase 00

| Tiêu chí | Bằng chứng trong tài liệu |
| --- | --- |
| Có luồng từ vào game đến kết quả, gồm đường thất bại | Mục 5–9; W-01, W-02, W-07, W-08 |
| Đủ 4 vai trò và mục tiêu teamwork, không đổi thành sản phẩm solo | Mục 2, 4, 6, 7; W-03, W-05 |
| Phạm vi riêng cho vertical slice, dungeon offline, multiplayer MVP | Mục 10; solo chỉ là mốc kiểm chứng trước khi đủ class/network |

## 15. Bàn giao cho các phase sau

- [Phase 01 — Combat design](../phases/phase-01-combat-design.md): đọc mục 3, 8, 9 và O-01/O-02; cụ thể hóa stat, damage, trạng thái, cast, hit timing và luật cứu theo C-05 đã xác nhận. GDD không cung cấp multiplier hoặc thời gian giả như thể đã chốt.
- [Phase 02 — Class design](../phases/phase-02-class-design.md): dùng mục 4, P-05 và COMBAT khi đã tồn tại để chọn bộ skill MVP. Không thiết kế bộ skill thiếu khả năng giải quyết cơ chế riêng.
- [Phase 03 — Boss design](../phases/phase-03-boss-mechanic-design.md): dùng mục 7–9 và O-03 để tách boss solo/team, xử lý class gục/thiếu, mechanic failure và kết quả cuối.
- [Phase 04 — Client bootstrap](../phases/phase-04-client-bootstrap.md): chỉ bắt đầu khi được giao triển khai và có đầu ra thiết kế cần thiết của Phase 00–03; dùng C-04 cùng input/góc nhìn trước khi chọn cấu hình client.

Nhiệm vụ hiện tại kết thúc ở tài liệu Phase 00 và cập nhật trạng thái liên quan. Không tạo COMBAT, CLASSES, BOSS-GOLEM, scaffold hoặc asset trong lượt này.
