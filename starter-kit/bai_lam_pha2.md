# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:** Võ Phan Đăng Khoa 
- **Lớp:** HCM_KS26_CNTT1
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):** Gemini

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**KET QUA AI**

```text
[
  {
    "ma_buffet": "NUONG",
    "ngay_dat": "2026-12-19",
    "nguoi_lon": 2,
    "tre_em": 1,
    "khu_vuc": "trong_nha",
    "ghi_chu": null
  },
  {
    "ma_buffet": "HAISAN",
    "ngay_dat": "2027-01-03",
    "nguoi_lon": 3,
    "tre_em": 0,
    "khu_vuc": null,
    "ghi_chu": "Một người dị ứng sữa"
  },
  {
    "ma_buffet": "LAU",
    "ngay_dat": null,
    "nguoi_lon": 4,
    "tre_em": 0,
    "khu_vuc": "san_vuon",
    "ghi_chu": "ông ngoại đi xe lăn"
  }
]
```

**Link trò chuyện:** https://share.gemini.google/8DzbZ8rHK8dp

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
Dưới đây là chi tiết các bước tính toán báo giá cho yêu cầu đặt bàn của đoàn:

**Bước 1: Xác định đơn giá gói buffet**

* Gói buffet lựa chọn: **NUONG – Buffet nướng**
* Đơn giá người lớn: 399.000 đồng/người

**Bước 2: Tính tiền buffet cho người lớn**

* Số lượng người lớn: 10 người
* Tiền buffet người lớn = 10 × 399.000 = 3.990.000 đồng

**Bước 3: Tính tiền buffet cho trẻ em**

* Nhóm trẻ em cao từ 1 m đến 1,4 m (tính 50% giá người lớn): 3 trẻ em (cao 1,1 m, 1,2 m và 1,35 m)
* Đơn giá trẻ em từ 1 m đến 1,4 m = 399.000 × 50% = 199.500 đồng/trẻ
* Tiền buffet nhóm trẻ em này = 3 × 199.500 = 598.500 đồng


* Nhóm trẻ em cao dưới 1 m (miễn phí): 1 bé (cao 0,8 m)
* Tiền buffet nhóm trẻ em này = 1 × 0 = 0 đồng


* Tổng tiền buffet trẻ em = 598.500 + 0 = 598.500 đồng

**Bước 4: Tính tổng tiền buffet trước khi giảm giá**

* Tổng tiền buffet trước giảm = Tiền buffet người lớn + Tiền buffet trẻ em
* Tổng tiền buffet trước giảm = 3.990.000 + 598.500 = 4.588.500 đồng

**Bước 5: Tính chiết khấu và tiền buffet sau giảm giá**

* Điều kiện áp dụng: Đoàn có 10 người lớn (đạt mức từ 10 người lớn trở lên) nên được giảm 5% trên tổng tiền buffet.
* Số tiền được giảm = 4.588.500 × 5% = 229.425 đồng
* Tiền buffet sau giảm = 4.588.500 - 229.425 = 4.359.075 đồng

**Bước 6: Tính phí phụ thu phòng riêng**

* Số lượng phòng riêng thuê: 1 phòng
* Phụ thu phòng riêng (không áp dụng giảm giá) = 1 × 500.000 = 500.000 đồng

**Bước 7: Tính tổng tiền thanh toán cuối cùng**

* Tổng tiền = Tiền buffet sau giảm + Phụ thu phòng riêng
* Tổng tiền = 4.359.075 + 500.000 = 4.859.075 đồng

[RESULT:4.859.075 đồng]
```

**Link trò chuyện:** https://share.gemini.google/7vnan68hn7l9

### b) Kiểm tra kết quả AI

AI đúng

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI** 

```text
{
  "loai_su_co": "thieu_mon",
  "so_khach": 5,
  "so_mon_bi_thieu": 2,
  "tom_tat": "Khách đi 5 người dùng buffet tối 08/11/2026 phản ánh hết tôm hùm và cua suốt buổi."
}
```

**Link trò chuyện:** https://share.gemini.google/zoLY2yf4J0z4

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**
