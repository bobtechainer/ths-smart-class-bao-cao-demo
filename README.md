# Báo cáo sau tiết học Smart Class

Hai trang HTML báo cáo cho một tiết học trên Smart Class: một trang cho giáo viên, một trang cho học sinh. Làm để đề xuất giao diện mới cho màn báo cáo cuối giờ trong `prj-ths-smart-class`. Hai trang đứng riêng, chưa gắn vào app đó. Tiết mẫu là Toán 7, lớp 7A3, bài Đại lượng tỉ lệ thuận, ngày 25/08/2026.

Người làm: Bob (BobLe, bob@techainer.com), tháng 8/2026 (làm trong ngày 25/08). Tình trạng: bản demo, đã đưa lên Vercel.

## Mở hoặc chạy thế nào

Không cần cài gì. Mở thẳng file bằng trình duyệt:

- `bao-cao-giao-vien.html`: trang cho giáo viên
- `bao-cao-hoc-sinh.html`: trang cho học sinh (nhật ký tiết học của em Minh Anh, chính là em Phạm Minh Anh trong bảng lớp ở trang giáo viên)

Nút VI/EN ở thanh trên cùng chuyển sang bản tiếng Anh (`*-en.html`). Trang có tải font Be Vietnam Pro từ Google Fonts, mất mạng thì trình duyệt dùng font thay thế.

Bản đang chạy trên Vercel (tài khoản Vercel của Bob, `bob-8053`):

- Giáo viên: https://bao-cao-tiet-hoc-gv.vercel.app (tiếng Anh: `/en.html`)
- Học sinh: https://bao-cao-tiet-hoc-hs.vercel.app (tiếng Anh: `/en.html`)

## Trong repo có gì

| File, thư mục | Để làm gì |
|---|---|
| `bao-cao-giao-vien.html` | Bản gốc tiếng Việt, trang giáo viên. Sửa nội dung ở đây trước. |
| `bao-cao-hoc-sinh.html` | Bản gốc tiếng Việt, trang học sinh. |
| `bao-cao-giao-vien-en.html`, `bao-cao-hoc-sinh-en.html` | Bản tiếng Anh, dịch từ hai file trên. |
| `deploy/bao-cao-tiet-hoc-gv/`, `deploy/bao-cao-tiet-hoc-hs/` | Bản đã đưa lên Vercel. `index.html` là tiếng Việt, `en.html` là tiếng Anh. Nội dung giống file gốc, chỉ khác link nút VI/EN. |
| `report-teacher-en.html`, `report-student-en.html` | Bản tiếng Anh đầu tiên (25/08, 10:38). Đã cũ, vẫn còn chỉ số "mức tập trung" mà bản sau đã bỏ. Giữ lại để đối chiếu. |
| `ban-nhap-cu/` | Bản nháp ngày 25/08/2026, làm trước khi có bản chính. Chép nguyên từ thư mục `bao-cao-smart-class-demo/` trên máy Bob, nên thư mục đó không cần đưa lên riêng. Bài khác hẳn: giáo viên là tiết Tiếng Anh 8A2, học sinh là tiết Vật lí 8. Không dùng nữa. |

Mỗi trang là một file HTML tự chứa. Biểu đồ vẽ bằng SVG trong file, không dùng thư viện biểu đồ, không có bước build.

Trang giáo viên có:

- nhịp tiết học theo từng phút
- em nào đã phát biểu, em nào chưa (bấm vào biểu đồ để lọc danh sách lớp)
- kết quả từng câu quiz, kèm phương án các em chọn sai
- game ôn tập cuối giờ
- bảng từng em và ba gợi ý cho tiết sau

Trang học sinh có:

- các lần em tham gia trong tiết
- so với chính em qua 5 tiết Toán gần nhất
- dạng bài đã chắc và chưa chắc
- phần thử lại câu 2
- hai việc cô giao

## Dữ liệu

Toàn bộ là dữ liệu giả lập. Hai trang chính gõ tay số liệu trong file HTML. Bản nháp trang giáo viên trong `ban-nhap-cu/` chỉ gõ tay tên. Số liệu từng em do đoạn script trong trang sinh ngẫu nhiên, lần nào mở cũng ra giống nhau. Không lấy từ production, UAT hay file của trường nào.

- Tên học sinh, tên giáo viên (Nguyễn Thu Hằng), lớp 7A3, phòng học đều là tên bịa.
- Khung số liệu dựng theo cấu trúc mock có sẵn trong `prj-ths-smart-class` (`src/analytics/mock/sessionMock.ts`): tiết 45 phút, lớp 25 em, 3 câu quiz, 1 game 10 câu. Tên trong mock đó khác, ở đây đặt lại cho tự nhiên.
- Một phần số liệu đã khớp nhau: 107 lượt phát biểu = 45 giơ tay + 42 trả lời + 20 câu hỏi, bằng tổng số lượt của 23 em trong bảng lớp. Số em có mặt, đi muộn, vắng và số em đã phát biểu cũng khớp bảng lớp.
- Trang giáo viên vẫn còn vài chỗ lệch với bảng lớp:
  - trang ghi 1.550 điểm thưởng, cột Điểm thưởng cộng lại là 1.775
  - trang ghi 5 em đúng cả 10 câu game, bảng chỉ có 2 em
  - trang ghi trung bình 7,2 câu game, bảng ra khoảng 7,0
  - ba câu quiz có 57 lượt đúng, cột Quiz cộng lại là 48
  - em Trần Khánh Vy mang nhãn "cần để ý thêm" dù không đúng điều kiện ghi trên trang
- Bản tiếng Anh và hai file trong `deploy/bao-cao-tiet-hoc-gv/` lệch y như vậy. Sửa số nào thì kiểm lại các chỗ liên quan ở cả bốn file của trang giáo viên.

Trên trang cố ý không có chữ "demo" hay "mô phỏng", vì lúc làm cần trông như sản phẩm đang chạy. Người xem link Vercel sẽ không biết đây là số liệu giả, nên khi gửi link nhớ nói trước. Dòng cuối mỗi trang ghi báo cáo đã lưu vào hệ thống LMS của Trường học số quốc gia. Câu đó cũng chỉ để trông như thật, hiện chưa nối với hệ thống nào.

## Không có trong repo

- Hai thư mục `.vercel/` trong `deploy/`: file liên kết thư mục với dự án Vercel trên máy Bob, có mã dự án và mã tài khoản. Vercel khuyên không chia sẻ.
- Các script dịch và chép bản deploy (`build-en.js`, `deploy-prep.js`): lúc làm để trong thư mục tạm, nay đã mất.

## Lưu ý cho người nhận

- Cách cập nhật khi không còn script: sửa file tiếng Việt gốc, sửa tay bản `-en` tương ứng, rồi chép sang `deploy/<thư mục>/index.html` và `en.html`. Nhớ đổi link nút VI/EN thành `index.html` và `en.html`.
- Đưa lên Vercel: `vercel deploy --prod --yes --cwd deploy/bao-cao-tiet-hoc-gv` (tương tự cho `-hs`). Máy khác phải `vercel link` lại vào dự án của mình, vì `.vercel/` không có trong repo.
- Khi dịch, nhớ tìm cả chữ tiếng Việt không dấu còn sót (" em", "lop", "cau"), không chỉ chữ có dấu.
- Mấy điều đã chốt trong lúc làm, đừng làm ngược:
  - Trang học sinh không có bảng xếp hạng, chỉ so với chính em.
  - Trang học sinh viết giọng hệ thống, xưng "bạn".
  - Đã bỏ nút "Xem lại tiết học", đừng thêm lại.
  - Chỉ số "Mức hoạt động trên máy" đếm số em đang bấm máy. Lúc cô giảng mà chỉ số thấp là bình thường.
- Logo là phần biểu tượng (3 nét đầu) trong `prj-ths-smart-class/public/logo.svg`, chép thẳng vào trang dạng SVG. Màu theo bộ Untitled UI bản MobiFone.
- Bước tiếp theo từng tính đến: đưa báo cáo từng tiết về hệ thống LMS của Trường học số quốc gia. Chưa làm.
