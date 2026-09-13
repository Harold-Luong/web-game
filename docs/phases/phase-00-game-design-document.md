# Phase 00 — Game Design Document

[README dự án](../../README.md) · [Hướng dẫn agent](../../AGENTS.md)

| Thuộc tính | Giá trị |
| --- | --- |
| Nhóm | A — Thiết kế trước khi code |
| Trạng thái công việc | DONE — hoàn thành đầu ra tài liệu GDD v0.1 và kiểm chứng trên giấy |
| Loại nhiệm vụ | Thiết kế bằng tài liệu |

Phase 00 đã có đầu ra [GDD v0.1](../design/GDD.md). DONE ở đây là hoàn thành tài liệu và checklist phía dưới; chưa có code, chưa kiểm chứng gameplay và không coi các đề xuất còn mở là đã được người dùng duyệt. Các mục giao việc được giữ lại để truy vết phạm vi.

## Mục tiêu

Chốt concept, core loop, phạm vi MVP, nền tảng, cách thắng/thua và điểm còn mở.

## Đầu vào và phụ thuộc

- Không phụ thuộc phase triển khai; cần yêu cầu sản phẩm trong README và thông tin người dùng đã cung cấp.

Đọc đầu ra và bằng chứng thực tế của các phase phụ thuộc, không chỉ file giao việc. Danh sách trên là phụ thuộc chính; thứ tự roadmap vẫn là mặc định. Nếu thiếu phần cần thiết, ghi rõ phần thiếu và chỉ làm phần độc lập trong nhiệm vụ, không tự triển khai toàn bộ phase trước.

**Đã xác nhận:** top-down trên máy tính với bàn phím/chuột; hết HP thì gục, đồng đội có thể cứu, cả đội gục thì thua. Phím cụ thể, targeting, quy tắc đúng một người mỗi class và chi tiết revive được bàn giao trong sổ quyết định GDD; chưa tự bắt đầu phần triển khai phụ thuộc.

## Các bước thực hiện

1. Xác định nền tảng, góc nhìn, input và vòng chơi; phân biệt sản phẩm co-op với prototype Warrior solo.
2. Mô tả đội hình, chọn class, bắt đầu dungeon, thắng/thua, chết/revive và chơi lại.
3. Chia MVP và phần ngoài MVP; ghi quyết định đã chốt, giả thuyết và câu hỏi cần người dùng quyết định.

## Đầu ra và phạm vi file

- Đầu ra đã tạo: [docs/design/GDD.md](../design/GDD.md), phiên bản 0.1.
- Đã cập nhật [README.md](../../README.md) để liên kết GDD, ghi nhận lựa chọn người dùng và tiến độ đúng thực tế.
- Báo cáo nghiệm thu nằm ở cuối file này; chưa tạo code, asset hoặc tài liệu đầu ra của Phase 01–03.

## Không làm trong phase này

Code, scaffold, asset, công thức combat chi tiết và thiết kế hạ tầng.

Không tự chuyển sang phase kế tiếp, thêm tính năng ngoài phạm vi hoặc tạo sẵn mọi module tương lai.

## Ràng buộc kiến trúc và phạm vi

Chỉ viết tài liệu thiết kế. Đánh dấu đề xuất và quyết định còn mở; không coi đặc tả giao việc này là đầu ra thiết kế đã hoàn thành.

Tuân theo [AGENTS.md](../../AGENTS.md). Giữ nguyên yêu cầu 4 vai trò trong sản phẩm cuối; chi tiết chưa chốt phải được ghi là giả thuyết/đề xuất, không tự coi thành quyết định của người dùng.

## Checklist nghiệm thu

- [x] GDD có luồng từ vào game đến kết quả, gồm cả đường thất bại — mục 5–9, walkthrough W-01/W-02/W-07/W-08.
- [x] Đủ 4 vai trò và mục tiêu teamwork; không tự đổi thành sản phẩm solo — mục 2/4/6/7 và walkthrough W-03/W-05.
- [x] Có phạm vi riêng cho vertical slice, dungeon offline và multiplayer MVP — bảng mốc tại mục 10.

Chỉ đánh dấu sau khi có bằng chứng. Nếu điều kiện hoặc môi trường còn thiếu, giữ chưa đạt và nêu giới hạn; không lấy build thành công thay cho kiểm chứng tương tác.

## Cách kiểm chứng

Đọc thử một lượt thắng, một lượt team wipe và một trường hợp thiếu class theo GDD; mỗi bước phải có kết quả hoặc câu hỏi còn mở được chỉ rõ.

Kiểm tra liên kết, thuật ngữ và sự nhất quán với README/các đặc tả liên quan. Không tạo code hoặc dependency chỉ để kiểm tra tài liệu.

## Lệnh giao việc cho AI

> Đọc README.md, AGENTS.md và docs/phases/phase-00-game-design-document.md. Thực hiện chỉ Phase 0 trong phạm vi đã mô tả. Kiểm tra đầu ra các phụ thuộc trước khi bắt đầu; không tự làm phase khác để lấp phần thiếu. Hoàn thành các bước được giao, kiểm chứng checklist, cập nhật báo cáo trong file phase và nêu rõ phần còn thiếu. Giữ các đề xuất chưa chốt ở trạng thái đề xuất.

Nếu chỉ muốn tiếp tục review tài liệu, thêm vào yêu cầu: **“Chỉ rà soát/cập nhật tài liệu Phase 0, chưa triển khai code.”**

## Báo cáo sau khi thực hiện

- Trạng thái: DONE — phạm vi tài liệu Phase 00; milestone M0 vẫn cần Phase 01–03.
- Quyết định đã xác nhận từ người dùng: C-04 (top-down, máy tính, bàn phím/chuột) và C-05 (gục/cứu đồng đội, cả đội gục thì thua), ngoài concept bốn vai trò đã có.
- Giả thuyết/đề xuất còn mở: đúng một người mỗi class, basic + hai skill, một dungeon 10–20 phút, retry từ đầu, chính sách thiếu người/disconnect và ưu tiên kết quả đồng thời. Chúng được gắn mã P/O trong GDD; không báo thành yêu cầu đã duyệt.
- File thực tế: tạo `docs/design/GDD.md`; sửa `README.md` và file Phase 00 này. Chưa sửa code, cấu hình chạy hoặc tạo asset.
- Kiểm chứng nội dung: walkthrough trên giấy W-01–W-10; lượt thắng có điểm kết thúc, team wipe có đường chơi lại, thiếu class bị chặn ở lobby, solo không đòi hệ revive team. W-05/W-06/W-09 chỉ rõ chi tiết chưa chốt ở phase sau.
- Kiểm chứng cấu trúc: đọc UTF-8, 15 mục GDD, 10 walkthrough, 17 mã quyết định không trùng, liên kết nội bộ/anchor hợp lệ; `git diff --check` không có lỗi whitespace. Đây là kiểm tra tài liệu, không phải chạy game/test runtime.
- Checklist: cả ba tiêu chí Phase 00 đạt ở mức tài liệu. Chưa có bằng chứng chơi thử về độ vui, thời lượng hoặc balance.
- Bàn giao: Phase 01 dùng GDD mục 3/8/9 và O-01/O-02 để thiết kế combat cùng revive; Phase 02 chọn bộ skill; Phase 03 cụ thể hóa cơ chế boss. Phím, targeting và quy tắc phụ thuộc cần chốt trước khi triển khai phần tương ứng. Không tự bắt đầu các phase này.

