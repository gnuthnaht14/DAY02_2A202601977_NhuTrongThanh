# 01 — Individual Problem Scan

## Scan rộng

Scan 8 problems.

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Lặp lại | Mỗi ngày phải nghe lần lượt nhiều voice message trong nhóm Zalo/Messenger để tổng hợp lại báo cáo | team member, lead | Lặp lại mỗi ngày, tốn 30 phút |
| 2 | Tốn thời gian | Sau cuộc họp dài, phải ghi và tóm tắt lại danh sách công việc | PM, team member, team leader | Bản ghi dài 30-60 phút; mất thêm khoảng 40-60 phút để viết recap |
| 3 | Lặp lại | Nhân viên CSKH nghe voice khách hàng và nhập lại vào hệ thống ticket | Team member, Nhân viên | Mỗi voice tốn khoảng 5-8p để nghe, ghi và phân loại |
| 4 | AI có thể làm tốt hơn | Công cụ chuyển voice thành văn bản tạo transcript dài nhưng không chỉ ra ý chính, deadline và người chịu trách nhiệm | PM, team member | tốn thời gian transcript+đọc lại để tóm tắt |
| 5 | Gián đoạn | Người đang họp, học hoặc ở nơi công cộng không thể mở voice message ngay nên phản hồi công việc bị chậm | Nhân viên, sinh viên | Voice thường được nghe sau khoảng 1-2h, ảnh hưởng tới công việc chung |
| 6 | AI có thể tốt hơn | Người dùng khó tìm lại một quyết định cũ vì nội dung nằm trong voice message và không thể tìm bằng từ khóa | Cả team | 10-15 phút/lần tìm |
| 7 | Pain từ người khác | Trưởng nhóm nhận báo cáo bằng voice từ nhiều thành viên nhưng khó tổng hợp nhanh trạng thái, rủi ro và việc cần hỗ trợ | PM, team leader | Hỏi lại 2-3 lần/spec |
| 8 | Pain từ người khác | Người lớn tuổi học người có vấn đề về thính giác không thể tiếp nhận thông báo và hướng dẫn | Người lớn tuổi, người thính lực yếu | Phải download các voice và sử dụng phần mềm thứ 3 |

## Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Voice to ticket | Workflow rõ, đọc lại và phân loại lâu, có metric tốt | Đưa human-in-loop để verify như thế nào |
| 2 | Tóm tắt buổi họp | Có pain thật, AI có thể giúp đọc/tóm tắt | Khó đo được chất lượng của tóm tắt |
| 3 | Người dùng khó tìm lại một quyết định cũ vì nội dung nằm trong voice message và không thể tìm bằng từ khóa | Nhiều người đau, impact rộng | Data access khó, bản thân việc tìm lại và tổng hợp voice từ các nền tảng đều khó |

## Problem Card #1 — Voice to ticket

**Problem 1 câu:**  
Nhân viên chăm sóc khách hàng lặp lại quá nhiều voice khiếu nại, mỗi voice phải nghe đi nghen lại tầm 2-3 lần/voice 5-6p để viết được ticket và phân loại.

**Actor:**  
Nhân viên CSKH chịu trách nhiệm viết ticket và phân loại để xử lý cho người dùng.

**Thời điểm / bối cảnh:**  
Hằng ngày, lặp lại mỗi khi có yêu cầu hoặc khiếu nại mới.

**Current workflow:**

```text
1. Nghe toàn bộ
2. Nghe lại đoạn chưa rõ
3. Ghi nội dung chính
4. Xác định các metadata của yêu cầu(loại vấn đề, mức độ ưu tiên,...)
5. Nhập ticket
6. Self-review + format
7. Gửi cho bộ phận quản lý
```

**Bottleneck:**  
Bước 4-5: tóm tắt, phân loại và nhập các thông tin theo cấu trúc ticket

**Metrics có thể đo:**  
Thời gian xử lí mỗi voice
Số voice xử lý được mỗi ngày
Tỉ lệ ticket phải nghe lại hoặc chỉnh sửa
Tỉ lệ phân loại ticket đúng

**Success metric:**  
Giảm tổng thời gian từ nghe 2-3 lần/voice 5-6p + phân loại nhập liệu -> mỗi ticket khoảng 20p. Giảm xuống còn 2p cho mỗi ticket.

**Non-AI alternative:**  
Các form cố định từ khóa phân loại có thể tạm thời hỗ trợ giảm thời gian nhưng không thể trích xuất và tự nhập dữ liệu như workflow

**AI hypothesis:**  
AI hỗ trợ cấu trúc dữ liệu và điền form, nhân viên vẫn cần check/review trước khi gửi.

**Quick gut:**  
Workflow.

### Draft current workflow

```text
CURRENT STATE — 26 phút

[1 Nghe voice: 8'] <-- bottleneck
→ [2 Tóm tắt: 5']
→ [3 Tổng hợp vào Docs: 5']
→ [4 Viết ticket: 5']
→ [5 Review + format: 2']
→ [6 Gửi: 1']
```

### Draft future workflow

```text
FUTURE STATE — 5 phút

[1 Auto-read data: 30s]
→ [2 AI tóm tắt nội dung: 1']
→ [3 AI nhập thông tin: 30s]
→ [4 PM review + edit: 2']  <-- human boundary
→ [5 PM gửi: 1']

Fallback: AI draft tệ → Nhân viên CSKH tự viết lại.
```

## Problem Cards #2 và #3 — tóm tắt

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn làm #1 |
|---|---|---|---|---|---|
| Tổng hợp báo cáo tiến độ từ voice | Trưởng nhóm, quản lý dự án | Phải nghe voice của từng thành viên, ghi tiến độ, blocker và action item rồi tổng hợp lại | Thời gian tổng hợp; số action item bị bỏ sót; số câu hỏi phải hỏi lại | Workflow | Cần xử lý nhiều người nói, nội dung không đồng nhất và thông tin phụ thuộc ngữ cảnh |
| Tìm lại quyết định cũ trong voice message | Thành viên nhóm, trưởng nhóm, PM | Không thể tìm bằng từ khóa nên phải nhớ vị trí hoặc nghe lại nhiều voice cũ | Thời gian tìm; số voice phải nghe lại; số lần phải hỏi lại; tỷ lệ tìm đúng quyết định | Agent / Workflow | Data access khó; voice nằm trên nhiều nền tảng; phạm vi tìm kiếm và tổng hợp có thể quá rộng |