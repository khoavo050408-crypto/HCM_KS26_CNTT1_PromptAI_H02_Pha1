# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:** Võ Phan Đăng Khoa
- **Lớp:** HCM_KS26_CNTT1
- **Link repository Pha1:** https://github.com/khoavo050408-crypto/HCM_KS26_CNTT1_PromptAI_H02_Pha1.git

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng [TEN_KHACH], số điện thoại [SĐT], số CCCD [SO_CCCD], email [EMAIL_KHACH], đặt bàn buffet hải sản (mã HAISAN) tối ngày 27/12/2026 cho 4 người lớn và 2 trẻ em. Khách đã chuyển khoản đặt cọc 1.000.000 đồng. Khách yêu cầu bàn gần cửa sổ.

```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
Câu 1 : Chỉ trả lời dựa trên nội dung của file chính sách đính kèm, tuyệt đối không sử dụng kiến thức bên ngoài hay tự suy diễn; nếu trong file không có thông tin hoặc không quy định rõ, hãy trả lời đúng nguyên văn: "Tài liệu đính kèm không có thông tin về vấn đề này."
Câu 2 : Hãy ghi rõ câu trả lời được trích xuất từ mục, khoản hoặc điều nào cụ thể trong file đính kèm.
```

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**PROMPT**

```text
CONTEXT
Bạn là chuyên gia phân loại tin nhắn của nhà hàng Bếp Việt Buffet

Request
Hãy chuyển TN1,TN2,TN3 thành 1 mảng JSON thành 3 đối tượng , đúng thứ tự , đúng 6 trường như tin nhắn mẫu

Explantation
1. ma_buffet lấy theo bảng mã loại buffet.

<ma_buffet>
BẢNG MÃ BUFFET
LAU – Buffet lẩu
NUONG – Buffet nướng
HAISAN – Buffet hải sản
</ma_buffet>

2. ngay_dat dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
4. khu_vuc chỉ nhận "trong_nha", "san_vuon" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về ăn uống, dị ứng, đi lại; không có thì null.

Action
1. yêu cầu tin nhắn mẫu nếu chưa được cung cấp
2. quét tìm các ý chính (quan trọng ) trong tin nhắn
3. đưa ra kết quả 

TONE 
Giọng điệu chuyên nghiệp không sử dụng các từ ngữ mang sắc thái cảm xúc vào kết quả 

Extras
Đưa kết quả thành 1 ĐỐI TƯỢNG JSON SẠCH (KHÔNG CHÀO HỎI , KHÔNG GIẢI THÍCH , CHỈ ĐƯA 1 BẢNG JSON THEO YÊU CẦU)

đây là các tin nhắn mẫu và kết quả mong muốn
Tin nhắn mẫu 1:
Đặt giúp em buffet hải sản tối 14/11/2026, 2 người lớn 2 bé, ngồi sân vườn. 1 bé dị ứng tôm.
Kết quả đúng:
{"ma_buffet": "HAISAN", "ngay_dat": "2026-11-14", "nguoi_lon": 2, "tre_em": 2, "khu_vuc": "san_vuon", "ghi_chu": "1 bé dị ứng tôm"}

Tin nhắn mẫu 2:
Buffet lẩu còn bàn trong nhà không shop, mình đi 1 người, hôm nào cũng được.
Kết quả đúng:
{"ma_buffet": "LAU", "ngay_dat": null, "nguoi_lon": 1, "tre_em": 0, "khu_vuc": "trong_nha", "ghi_chu": null}

tin nhắn cần xử lý 
<tin_nhan>
TN1: Cho mình đặt buffet nướng ngày 19/12 nha, 2 người lớn với 1 bé 9 tuổi, ngồi trong nhà.

TN2: Đặt bàn buffet hải sản cho 3 người ngày 03/01/2027 ạ. Một người dị ứng sữa.

TN3: Buffet lẩu tối Giáng sinh còn bàn không ạ? Nhà em 4 người lớn, ông ngoại đi xe lăn, ngồi sân vườn.
</tin_nhan>
```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Context
Bạn là chuyên gia tính tổng tiền cho yêu cầu báo giá của nhà hàng Bếp Việt Buffet

Request
Bạn sẽ dựa vào yêu cầu đặt bàn của khách và tính tổng tiền sau khi thực hiện các bước tính toán theo quy tắc "thinking step by step"

Explanation
1.LUÔN THỰC HIỆN VÀ ĐƯA RA KẾT QUẢ TỪNG BƯỚC TRƯỚC KHI ĐƯA RA BƯỚC TIẾP THEO 
2. luôn dựa vào bảng giá được cung cấp
<bang_gia>
BẢNG GIÁ BUFFET (đồng/người lớn)
LAU – Buffet lẩu: 299.000
NUONG – Buffet nướng: 399.000
HAISAN – Buffet hải sản: 599.000
</bang_gia>
3. không tự ý tạo ra thêm các chương trình khi khách yêu cầu mà lịch sự giải thích cho khách hàng rằng giá được niêm phong và không thể thay đổi

4. đay là bộ quy tắc luôn áp dụng cho mọi trường hợp và không bao giờ có ngoại lệ
<quy_tac_tinh_tien>
QUY TẮC TÍNH GIÁ
1. Trẻ em cao từ 1 m đến 1,4 m tính 50% giá người lớn. Trẻ dưới 1 m miễn phí.
2. Đoàn từ 10 người lớn trở lên được giảm 5% trên tiền buffet (tiền người lớn + tiền trẻ em).
3. Phụ thu phòng riêng: 500.000 đồng/phòng. Phụ thu không được giảm giá.
4. Tổng tiền = tiền buffet sau giảm + phụ thu.
</quy_tac_tinh_tien>

Tone 
Giọng điệu chuyên nghiệp và không đưa các từ ngữ mang hàm ý cảm xúc vào

Extras
kết quả cuối cùng sau khi tính toán đưa ra dưới dạng
[RESULT:<tổng tiền> đồng]




```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
context
Bạn là 1 chuyên gia đọc email của nhà hàng Bếp Việc Buffet

request
hãy đọc email và lọc ra các khiếu nại của khách hàng theo các các trường quy định sau ở dạng 1 bảng JSON cố dịnh :
{"loai_su_co": một trong "thieu_mon" | "cho_lau" | "nhan_vien" | "khac"

 "so_khach": số nguyên, "so_mon_bi_thieu": số nguyên hoặc null
 
 "tom_tat": "không quá 20 từ"}

explanation
khi không có trường nào thì để là null
không tự ý thêm vào các chi tiết không được cung cấp

action 
1 đọc email
2 trả về kết quả

tone
đưa ra kết quả là 1 bảng json sạch theo yêu cầu

```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. kết quả có đúng định dạng không


2.có sai thông tin so với email của khách không

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
bạn đã dừng ở đoạn BẾP VIỆT buffet xin hoàn lại hãy tiếp tục làm theo yêu cầu không chào hỏi lại 
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text


## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Bếp Việt", nhân viên tư vấn trên website của nhà hàng Bếp Việt Buffet, giúp khách chọn và đặt bàn một trong 3 loại buffet: LAU (Buffet lẩu), NUONG (Buffet nướng), HAISAN (Buffet hải sản).

[Quy tắc ràng buộc]
1. chỉ tư vấn 3 loại buffet
2.không yêu cầu hay xin sđt hay số cccd , số thẻ ngân hàng
3.không hưa giảm giá ngoài chương trình

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá buffet trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: (Viết cách trả lời – xoá dòng này)
- Khách cung cấp thiếu thông tin:
```
