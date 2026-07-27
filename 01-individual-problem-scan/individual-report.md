# 01 — Individual Problem Scan

## Scan rộng

Scan 8 problems.

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Lặp lại | Mỗi ngày phải nghe lần lượt nhiều voice message trong nhóm Zalo/Messenger để tìm thông tin liên quan đến công việc | team member, lead | Lặp lại mỗi ngày, tốn 30 phút |
| 2 | Tốn thời gian | Sau cuộc họp dài, phải ghi và tóm tắt lại danh sách công việc | PM, team member, team leader | Bản ghi dài 30-60 phút; mất thêm khoảng 40-60 phút để viết recap |
| 3 | AI có thể làm tốt hơn | Liên kết voice với context hiện tại của chat | Team member, PM | Tốn thời gian vừa xem voice vừa đọc chat 30p-45p |
| 4 | AI có thể làm tốt hơn | Công cụ chuyển voice thành văn bản tạo transcript dài nhưng không chỉ ra ý chính, deadline và người chịu trách nhiệm | PM, team member | tốn thời gian transcript+đọc lại để tóm tắt |
| 5 | Gián đoạn | Người đang họp, học hoặc ở nơi công cộng không thể mở voice message ngay nên phản hồi công việc bị chậm | Nhân viên, sinh viên | Voice thường được nghe sau khoảng 1-2h, ảnh hưởng tới công việc chung |
| 6 | AI có thể tốt hơn | Người dùng khó tìm lại một quyết định cũ vì nội dung nằm trong voice message và không thể tìm bằng từ khóa | Cả team | 10-15 phút/lần tìm |
| 7 | Pain từ người khác | Trưởng nhóm nhận báo cáo bằng voice từ nhiều thành viên nhưng khó tổng hợp nhanh trạng thái, rủi ro và việc cần hỗ trợ | PM, team leader | Hỏi lại 2-3 lần/spec |
| 8 | Pain từ người khác | Người lớn tuổi học người có vấn đề về thính giác không thể tiếp nhận thông báo và hướng dẫn | Người lớn tuổi, người thính lực yếu | Phải download các voice và sử dụng phần mềm thứ 3 |

Vì sao phần scan này mạnh:

- Có scan rộng trước khi hội tụ.
- Có nhiều lăng kính khác nhau.
- Mỗi problem có actor và dấu hiệu thật.
- Không bắt đầu bằng "làm chatbot" hoặc "xây agent".

## Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Weekly Report | Workflow rõ, mất nhiều thời gian, có metric tốt | Narrative "đủ tốt" đo thế nào |
| 2 | Review PRD | Có pain thật, AI có thể giúp đọc/tóm tắt | Quality improvement khó đo |
| 3 | Slack Search | Nhiều người đau, impact rộng | Data access khó, scope có thể quá lớn |

## Problem Card #1 — Weekly Report

**Problem 1 câu:**  
Mỗi thứ Hai PM mất khoảng 90 phút tổng hợp Weekly Report từ nhiều nguồn, trong đó bước viết narrative tốn nhất và dễ trễ deadline.

**Actor:**  
Junior PM chịu trách nhiệm gửi weekly report cho Engineering Manager và CEO.

**Thời điểm / bối cảnh:**  
Thứ Hai hằng tuần, trước buổi leadership sync.

**Current workflow:**

```text
1. Export Jira sprint data
2. Lấy metrics từ Google Sheets
3. Đọc Slack recap tuần
4. Tổng hợp vào Google Docs
5. Viết narrative: insight, highlight, risk, next action
6. Self-review + format
7. Gửi email cho stakeholders
```

**Bottleneck:**  
Bước 5 — viết narrative từ raw data mất khoảng 25 phút và hay bị blank page.

**Impact:**  
90 phút/tuần cho 1 PM. Team có 3 PM nên tổng công sức có thể khoảng 270 phút/tuần. Báo cáo trễ làm leadership thiếu bối cảnh trước buổi sync.

**Success metric:**  
Giảm tổng thời gian từ 90 phút xuống dưới 30 phút, không tăng số câu CEO/EM phải hỏi lại.

**Non-AI alternative:**  
Template report + Jira dashboard + checklist có thể giảm format effort, nhưng chưa giải quyết tốt phần viết narrative.

**AI hypothesis:**  
AI hỗ trợ cấu trúc dữ liệu và draft narrative. PM vẫn review/edit trước khi gửi.

**Quick gut:**  
Workflow.

### Draft current workflow

```text
CURRENT STATE — 90 phút

[1 Export Jira: 10']
→ [2 Lấy metrics: 10']
→ [3 Đọc Slack: 15']
→ [4 Tổng hợp vào Docs: 15']
→ [5 Viết narrative: 25']  <-- bottleneck
→ [6 Review + format: 10']
→ [7 Gửi: 5']
```

### Draft future workflow

```text
FUTURE STATE — 21 phút

[1 Auto-pull data: 2']
→ [2 AI cấu trúc dữ liệu: 1']
→ [3 AI draft narrative: 1']
→ [4 PM review + edit: 15']  <-- human boundary
→ [5 PM gửi: 2']

Fallback: AI draft tệ → PM tự viết lại.
```

## Problem Cards #2 và #3 — tóm tắt

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn làm #1 |
|---|---|---|---|---|---|
| Review PRD | PM reviewer | Đọc 10-15 trang để hiểu context | 45 phút → 20 phút | Workflow | Quality metric khó hơn |
| Slack Search | Team member | Search keyword rồi đọc thread | 15 phút → dưới 2 phút | Agent / Workflow | Data access và scope rộng |

---