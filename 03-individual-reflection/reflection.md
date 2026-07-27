# 03 — Individual Reflection 

## Đóng góp của Thành trong nhóm

| Hoạt động | Thành đã làm gì? | Kết quả |
|---|---|---|
| Scan cá nhân | Đưa ra 8 problems | Nhóm có nhiều candidate về agent/workflow |
| Pitch | Pitch Voice to text CSKH | Bài được vào shortlist |
| Challenge | Hỏi nhóm lọc CV có thể lọc ứng viên ra sao? | Nhóm trình bày được cách để lọc ứng viên cụ thể nhất |
| Workflow | Vẽ current/future workflow cho voice to text | Nhóm ham khảo workflow của mình để đơn giản hóa workflow cho CV filtering |
| Research | Tìm các dịch vụ khác về lọc CV: topCV, VNworks | Nhóm thấy nên sử dụng workflow cho đơn giản hóa bước đầu |
| Rule / Workflow / Agent | Lập luận chọn Workflow, không chọn Agent | Nhóm thống nhất chọn workflow |

## Bảng dùng AI trong reflection

| Phase | Tôi dùng AI để làm gì? | AI hữu ích ở đâu? | AI sai/hời hợt ở đâu? | Tôi sửa gì |
|---|---|---|---|---|
| Scan | Gợi ý các problems trong phạm vi text-to-speech và tóm tắt voice message | Giúp mở rộng danh sách lên hơn 8 problems theo các lăng kính như lặp lại, tốn thời gian, khó tìm kiếm và pain từ người khác | Một số gợi ý ban đầu còn chung chung; dấu hiệu thật sử dụng số liệu giả định, chưa được kiểm chứng | Yêu cầu AI viết lại với actor, workflow và dấu hiệu cụ thể; chỉ giữ số liệu có thể xác nhận bằng log hoặc phỏng vấn |
| Workflow | Mô tả current workflow, bottleneck và metric cho các candidate problems | Giúp nhìn rõ chuỗi thao tác thủ công và vị trí AI có thể hỗ trợ phiên âm, tóm tắt hoặc phân loại | AI giả định một số bước và công cụ chưa chắc tồn tại trong workflow thực tế | Giữ workflow ở mức bản nháp, tách bước AI xử lý và bước con người review, đồng thời ghi rõ các giả định cần validation |
| Research | So sánh sơ bộ tính khả thi và rủi ro của các candidate problems | Chỉ ra các rủi ro như khó truy cập voice trên nhiều nền tảng, mất ngữ cảnh và bỏ sót quyết định | Chưa có research từ nguồn chính thức; một số nhận định về hiệu quả chưa được kiểm chứng | Không sử dụng claim chưa có nguồn; cần bổ sung phỏng vấn, log thực tế và tài liệu chính thức |
| Problem Statement | Chọn Top 3, viết problem một câu và tóm tắt Problem Cards #2, #3 | Giúp làm rõ actor, bottleneck, metric và điều còn chưa chắc của từng candidate | AI ban đầu chọn vấn đề TTS phát âm sai làm problem #3 nhưng chưa phù hợp với ưu tiên của tôi | Thay problem #3 bằng việc khó tìm lại quyết định cũ trong voice message và bổ sung rủi ro data access, scope đa nền tảng |

## Bài học của Thành

- Problem tốt không phải problem nghe "AI" nhất, mà là problem có workflow và metric rõ.
- Vẽ workflow giúp thấy phần nào rule đủ, phần nào AI mới có ích.
- Agent không phải đích đến mặc định. Trong case này, Workflow hợp lý hơn vì có đường đi cố định và có PM review.
- Research không phải để copy tool, mà để thấy pattern: nhiều sản phẩm tốt đều để AI draft, người thật review.

Nếu làm lại:

```text
Tôi sẽ thử nghiệm ngay với workflow đơn giản nhất để xem hiệu quả extract data từ pdf ra sao trước khi thực sự bắt tay vào làm.
```

---