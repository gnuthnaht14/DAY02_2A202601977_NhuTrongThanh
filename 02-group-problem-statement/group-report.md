# Group Report — Day 02

## Thành viên nhóm

| STT | Họ và tên | Mã học viên | Vai trò trong nhóm |
|-----|-----------|-------------|--------------------|
| 1   | Nhữ Trọng Thành | 2A202601977 | Thuyết trình+Đưa ý tưởng |
| 2   | Mai Hồng Sơn | 2A202601921 | Đưa ý tưởng |
| 3   | Lê Thị Linh | 2A202601441 | Đưa ý tưởng |
| 4   | Vũ Thu Huyền | 2A202601583 | Thuyết trình+Đưa ý tưởng |
| 5   | Lường Thị Hảo | 2A202601637 | Đưa ý tưởng |


# 02 — Group Problem Statement

## Group convergence

Nhóm 4-5 người, mỗi người share top 3. Tổng cộng khoảng 12-15 candidates.

| Cluster | Candidate examples | Pattern chung |
|---|---|---|
| Báo cáo / tổng hợp thông tin | Voice-to-task, Lọc CV | Gom thông tin từ nhiều nguồn rồi viết lại cho người khác đọc |
| Tìm kiếm / hỏi đáp tài liệu | Tìm lại voice cũ, lọc và đánh giá | Tìm đúng thông tin trong nhiều nguồn rời rạc |

Nhóm chọn: **Voice to task**.

Vì sao chọn:

- Có workflow rõ.
- Có baseline thời gian.
- Có thể validate với các dự án khác sẵn có.
- Có thể so sánh before/after rất rõ.

Vì sao không chọn các bài khác:

- Voice-to-task: Không validate được với các sản phẩm/tool có sẵn
- Coding-prompt(Anh Sơn): Quá rộng, chưa tìm được nỗi đau cụ thể.

## Quick validation

| Nguồn | Số người | Tín hiệu xác nhận | Tín hiệu phản bác | Nhóm sửa problem thế nào |
|---|---:|---|---|---|
| Quick interview | 3 | 2/3 người từng phải nghe lại voice của khách hàng, ghi nội dung chính rồi nhập thủ công vào ticket; phần tóm tắt và phân loại mất nhiều thời gian nhất | 1 người cho biết phần lớn khách hàng của họ gửi tin nhắn chữ nên voice không xuất hiện đủ thường xuyên | Thu hẹp đối tượng sang đội CSKH tiếp nhận nhiều yêu cầu qua Zalo, Messenger hoặc nền tảng hỗ trợ voice |
| Mini poll | 6 | 4/6 người từng bỏ sót chi tiết, phải nghe lại hoặc hỏi lại khi voice chứa nhiều yêu cầu trong cùng một tin nhắn | 2 người cho rằng voice ngắn có thể nghe trực tiếp, không cần AI tóm tắt | Chỉ áp dụng với voice dài hoặc chứa nhiều thông tin; AI tạo bản nháp ticket nhưng nhân viên vẫn kiểm tra trước khi lưu |
| Thử nghiệm với voice mẫu | 5 voice | Có thể trích xuất các trường chính như vấn đề, sản phẩm, mức độ ưu tiên và hành động mong muốn | Một số voice thiếu thông tin, có tiếng ồn hoặc diễn đạt không rõ nên bản tóm tắt chưa đáng tin cậy | Thêm trạng thái “thiếu thông tin”, giữ liên kết tới voice gốc và yêu cầu nhân viên xác nhận trước khi tạo ticket |

Insight sau validation:

```text
Pain thật không nằm ở việc nghe mọi voice message. Pain nằm ở bước chuyển những voice dài hoặc chứa nhiều yêu cầu thành ticket có cấu trúc mà không bỏ sót thông tin quan trọng.

Vì vậy, scope phù hợp không phải là tự động xử lý toàn bộ yêu cầu của khách hàng. Workflow chỉ phiên âm, tóm tắt và đề xuất thông tin cho ticket; nhân viên CSKH vẫn nghe lại khi cần, chỉnh sửa và xác nhận trước khi lưu hoặc chuyển ticket.
```

## Research giải pháp

Nhóm tìm các hướng đã có sẵn, không giả định phải tự build từ đầu.

| Nguồn / tool / case | Link | Họ giải quyết phần nào? | Điểm mạnh | Khoảng trống / rủi ro | Bài học cho nhóm |
|---|---|---|---|---|---|
| Google Cloud Speech-to-Text | https://docs.cloud.google.com/speech-to-text/docs/v1/speech-to-text-supported-languages?hl=en | Chuyển audio thành transcript; hỗ trợ tiếng Việt và nhận dạng voice ngắn hoặc dài | Có thể dùng model adaptation để cải thiện nhận dạng tên riêng và thuật ngữ chuyên ngành | Chỉ giải quyết bước voice → text, chưa tóm tắt, phân loại hoặc tạo ticket; transcript vẫn có thể sai khi audio nhiễu | Có thể dùng dịch vụ có sẵn cho bước phiên âm, không cần tự xây speech-to-text model |
| Amazon Transcribe Call Analytics | https://docs.aws.amazon.com/transcribe/latest/dg/call-analytics.html | Phiên âm và phân tích hội thoại khách hàng, gồm issue, action item, outcome, sentiment và tóm tắt | Có nhiều chức năng phù hợp với chăm sóc khách hàng và hỗ trợ xử lý dữ liệu nhạy cảm | Được thiết kế chủ yếu cho call-center audio và yêu cầu audio hai kênh; không trực tiếp phù hợp với voice message một người trên Zalo/Messenger | Pattern issue → action item → outcome có thể dùng để thiết kế cấu trúc bản nháp ticket |
| Microsoft Dynamics 365 Customer Service Copilot | https://learn.microsoft.com/en-us/dynamics365/contact-center/use/copilot-summarize-conversations | Tóm tắt chat hoặc voice conversation đã được phiên âm; cho phép tạo case và điền phần mô tả bằng summary | Gần với workflow voice → summary → case; nhân viên có thể chủ động bấm tạo case | Phụ thuộc hệ sinh thái Dynamics 365 và cấu hình của quản trị viên; không trực tiếp xử lý voice message từ nhiều nền tảng bên ngoài | Pattern phù hợp là AI tạo summary, còn nhân viên chủ động xác nhận và tạo case |
| Zendesk AI-generated ticket summaries | https://support.zendesk.com/hc/en-us/articles/8037565521946-Turning-on-and-configuring-AI-generated-ticket-summaries | Tóm tắt nội dung đã có trong ticket, gồm vấn đề, kỳ vọng của khách hàng, hành động, kết quả và trạng thái hiện tại | Cấu trúc summary sát với thông tin nhân viên CSKH cần để xử lý và bàn giao ticket | Bắt đầu từ comments và notes đã có trong ticket, chưa giải quyết bước lấy voice message và chuyển thành transcript | Nhóm có thể học cấu trúc output của Zendesk để xác định các field cần trích xuất từ voice |
| Dynamics 365 Case Management Agent | https://learn.microsoft.com/en-us/dynamics365/customer-service/administer/set-up-autonomous-case-agents | Trích xuất thông tin từ chat hoặc voice conversation để tạo và cập nhật case | Cho thấy khả năng tự động hóa sâu hơn, bao gồm dự đoán và điền các trường như mô tả, contact, product và priority | Tự tạo case có rủi ro nếu transcript hoặc thông tin được trích xuất sai; tính năng phụ thuộc nền tảng và cấu hình quyền | Agent là hướng mở rộng sau này; pilot ban đầu chỉ nên tạo draft để nhân viên kiểm tra |

Research takeaway:

```text
Không cần tự build mô hình speech-to-text hoặc một agent tự động xử lý toàn bộ yêu cầu.

Hướng phù hợp hơn là Workflow:

Voice message
→ dịch vụ speech-to-text tạo transcript
→ AI tóm tắt và trích xuất các trường của ticket
→ nhân viên CSKH kiểm tra, sửa và bổ sung thông tin
→ nhân viên xác nhận tạo hoặc chuyển ticket.

Human review là boundary bắt buộc vì transcript có thể sai, voice có thể thiếu ngữ cảnh và AI có thể phân loại nhầm. Chỉ nên cân nhắc Agent tự tạo hoặc tự chuyển ticket sau khi workflow nhỏ đã được kiểm chứng bằng dữ liệu thực tế.
```

## Draft current workflow

```text
CURRENT STATE — 26 phút

[1 Nghe voice: 8'] <-- bottleneck
→ [2 Tóm tắt: 5']
→ [3 Tổng hợp vào Docs: 5']
→ [4 Viết ticket: 5']
→ [5 Review + format: 2']
→ [6 Gửi: 1']
```

## Draft future workflow

```text
FUTURE STATE — 5 phút

[1 Auto-read data: 30s]
→ [2 AI tóm tắt nội dung: 1']
→ [3 AI nhập thông tin: 30s]
→ [4 PM review + edit: 2']  <-- human boundary
→ [5 PM gửi: 1']

Fallback: AI draft tệ → Nhân viên CSKH tự viết lại.
```text
Bottleneck mới:
PM review + edit. Đây là bottleneck chấp nhận được vì đó là điểm kiểm soát chất lượng.
```

Before/after impact:

| Metric | Trước | Sau kỳ vọng | Ghi chú |
|---|---:|---:|---|
| Thời gian xử lý trung bình | Khoảng 6 phút/voice | Dưới 3 phút/voice | Baseline cần được xác nhận bằng log thực tế |
| Số bước | 7 | 5 | Giảm effort ở bước nghe lại, tóm tắt và nhập ticket |
| Bước thủ công | 7/7 | 2/5 | Nhân viên CSKH vẫn review và xác nhận tạo ticket |
| Bottleneck chính | Nghe lại và nhập thông tin | Review/edit bản nháp | Human boundary |
| Rủi ro mới | Không có AI hallucination | Transcript sai, bỏ sót hoặc suy diễn thông tin | Cần đối chiếu voice trước khi tạo ticket |

## Problem Statement v0

| Field | Nội dung |
|---|---|
| **Actor** | Nhân viên chăm sóc khách hàng tiếp nhận yêu cầu bằng voice message qua Zalo, Messenger hoặc nền tảng hỗ trợ khách hàng. |
| **Workflow** | Nhân viên nhận voice → nghe toàn bộ → nghe lại đoạn chưa rõ → ghi nội dung chính → xác định loại vấn đề và mức ưu tiên → nhập ticket → chuyển cho bộ phận xử lý. |
| **Bottleneck** | Bước nghe lại, tóm tắt và nhập thông tin vào ticket mất phần lớn thời gian vì một voice có thể chứa nhiều yêu cầu, thiếu cấu trúc hoặc có đoạn khó nghe. |
| **Impact** | Mỗi voice mất khoảng 6 phút để xử lý; nhân viên phản hồi chậm hơn và có nguy cơ bỏ sót vấn đề, sản phẩm, deadline hoặc mong muốn của khách hàng. |
| **Success Metric** | Giảm thời gian xử lý trung bình từ khoảng 6 phút xuống dưới 3 phút/voice; không tăng số ticket thiếu trường quan trọng hoặc phải sửa sau khi tạo. |
| **Boundary** | AI không tự trả lời khách hàng, không tự tạo hoặc chuyển ticket, không tự suy diễn thông tin không có trong voice; nhân viên CSKH phải kiểm tra và xác nhận output cuối. |

## No AI / Rule / Workflow / Agent

| Mức | Phương án | Khi nào đủ | Rủi ro | Chọn? |
|---|---|---|---|---|
| **No AI** | Nhân viên nghe voice, ghi chú và nhập ticket thủ công | Đủ nếu số lượng voice ít, nội dung ngắn và không xuất hiện thường xuyên | Tốn thời gian, khó mở rộng và dễ bỏ sót thông tin khi volume tăng | Không chọn làm phương án chính, nhưng giữ làm fallback |
| **Rule** | Dùng form ticket cố định, checklist trường bắt buộc, macro và rule định tuyến theo từ khóa | Đủ nếu nội dung đã ở dạng text và các loại yêu cầu ít thay đổi | Không giải quyết được bước phiên âm và tóm tắt voice có cách diễn đạt đa dạng | Dùng cho kiểm tra field bắt buộc và định tuyến các trường hợp rõ |
| **Workflow** | Speech-to-text → AI tóm tắt và trích xuất field → đề xuất loại ticket → nhân viên review → xác nhận tạo ticket | Hợp vì workflow tuyến tính, output có cấu trúc và có điểm kiểm soát của con người | Transcript có thể sai; AI có thể bỏ sót hoặc phân loại nhầm | Chọn |
| **Agent** | Agent tự lấy voice, phân tích, hỏi thêm khách hàng, tạo và chuyển ticket tới bộ phận phù hợp | Chỉ cần khi hệ thống phải xử lý nhiều nhánh, dùng nhiều tool và tự quyết định bước tiếp theo | Scope rộng, cần nhiều permission; có thể tạo hoặc chuyển sai ticket và ảnh hưởng khách hàng | Chưa chọn |

Mức chọn:

```text
Workflow.
```

Vì sao:

- Speech-to-text có thể xử lý bước chuyển voice thành văn bản.
- AI phù hợp với bước tóm tắt và trích xuất thông tin từ cách diễn đạt không cố định.
- Rule và template vẫn hữu ích để kiểm tra trường bắt buộc và định tuyến các trường hợp rõ ràng.
- Nhân viên CSKH review trước khi tạo ticket nên rủi ro có thể kiểm soát.
- Chưa cần Agent vì pilot không cần AI tự liên hệ khách hàng hoặc tự quyết định chuyển ticket.

## Problem Statement v1

| Field | Nội dung |
|---|---|
| **Actor** | Nhân viên CSKH thường xuyên tiếp nhận yêu cầu của khách hàng bằng voice message. |
| **Workflow** | Nhận voice → nghe → nghe lại đoạn chưa rõ → tóm tắt → phân loại → nhập ticket → chuyển xử lý. |
| **Bottleneck** | Nghe lại và chuyển nội dung voice không có cấu trúc thành các field của ticket mất phần lớn thời gian, đồng thời dễ bỏ sót thông tin quan trọng. |
| **Impact** | Khoảng 6 phút xử lý cho mỗi voice; ticket có thể được tạo chậm, thiếu thông tin hoặc phải hỏi lại khách hàng. |
| **Success Metric** | Giảm thời gian xử lý trung bình xuống dưới 3 phút/voice; không tăng tỷ lệ ticket thiếu field quan trọng hoặc phải sửa sau khi tạo. Đo bằng log thời gian và checklist lỗi trong pilot. |
| **Boundary** | AI không tự trả lời khách hàng, không tự tạo hoặc chuyển ticket, không suy diễn thông tin không xuất hiện trong voice và chỉ xử lý dữ liệu được cung cấp. |
| **AI intervention point** | Sau khi nhân viên nhận voice và trước bước tóm tắt, phân loại, nhập thông tin vào ticket. |
| **Mức chọn** | Workflow: speech-to-text tạo transcript, AI draft ticket có cấu trúc, rule kiểm tra field, nhân viên CSKH review và xác nhận. |
| **Rủi ro & người thật kiểm tra** | Risk: phiên âm sai, bỏ sót yêu cầu, suy diễn priority hoặc phân loại nhầm. Người thật review: nhân viên CSKH đối chiếu transcript với voice, chỉnh các field và xác nhận trước khi tạo hoặc chuyển ticket. |

## Final decision

Decision:

```text
Go với scope nhỏ.
```

Pilot nhỏ nhất:

- Dùng 10–20 voice message tiếng Việt đã được ẩn thông tin cá nhân hoặc có quyền sử dụng.
- Chỉ thử nghiệm với một loại yêu cầu CSKH và một mẫu ticket cố định.
- Chạy workflow bán thủ công: nhân viên tải voice lên → speech-to-text tạo transcript → AI tóm tắt và điền bản nháp ticket.
- Bản nháp gồm các trường: vấn đề chính, sản phẩm/dịch vụ, mức ưu tiên đề xuất, hành động khách hàng mong muốn và thông tin còn thiếu.
- Nhân viên CSKH đối chiếu với voice gốc, chỉnh sửa và xác nhận; AI không tự trả lời khách hàng, tạo ticket hoặc chuyển ticket.
- Đo thời gian xử lý mỗi voice, số field phải sửa, số thông tin quan trọng bị bỏ sót và số nội dung AI suy diễn sai.

Exit / rollback:

- Nếu thời gian xử lý trung bình không giảm ít nhất 30% hoặc vẫn cao hơn 3 phút/voice sau hai vòng thử nghiệm, hạ xuống transcript + template ticket cố định.
- Nếu hơn 10% voice có lỗi nghiêm trọng như sai vấn đề, sản phẩm, deadline hoặc yêu cầu của khách hàng, không cho AI tạo bản nháp ticket để sử dụng trực tiếp.
- Nếu AI thường xuyên thêm thông tin không có trong voice, chỉ giữ speech-to-text và để nhân viên tự tóm tắt.
- Nếu không thể bảo đảm quyền sử dụng, ẩn dữ liệu cá nhân hoặc kiểm soát truy cập voice, dừng pilot.

Decision rationale:

- Problem có actor, workflow, bottleneck và metric rõ.
- Các dịch vụ speech-to-text và công cụ tóm tắt đã có sẵn nên không cần build mô hình từ đầu.
- Rule và template vẫn được dùng để kiểm tra field bắt buộc và hỗ trợ phân loại các trường hợp rõ ràng.
- AI chỉ nằm ở bước phiên âm, tóm tắt và tạo bản nháp, không ôm toàn bộ quy trình CSKH.
- Nhân viên CSKH luôn review và xác nhận nên rủi ro có thể kiểm soát.
- Chưa cần Agent vì pilot không yêu cầu AI tự hỏi khách hàng, tự tạo ticket hoặc tự quyết định nơi chuyển xử lý.

---
