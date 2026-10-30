# Bài 4: Tối ưu hóa lưu trữ dữ liệu doanh nghiệp

## Phần 1: Giải pháp kỹ thuật (Files On-Demand)

### 1.1 Vấn đề
- Cloud có 500GB video, SSD laptop chỉ 256GB.
- Đồng bộ toàn bộ (chế độ Mirror) thì SSD tràn, phần mềm đồng bộ bị treo.

### 1.2 Cách thiết lập Files On-Demand
1. Cài và đăng nhập **OneDrive** (hoặc Google Drive for desktop).
2. Bật tính năng:
   - OneDrive: Settings → Sync and backup → Advanced settings → bật **Files On-Demand**.
   - Google Drive: Preferences → Google Drive → chọn **Stream files**.
3. File video trên máy chỉ là **bản giữ chỗ** (hiện tên, dung lượng, biểu tượng đám mây), gần như không chiếm ổ cứng.
4. Khi mở file, hệ thống mới **tải về đúng file đó**.
5. Xong việc, chuột phải → **Free up space** (OneDrive) hoặc **Remove download** (Google Drive) để trả lại dung lượng.

### 1.3 Xử lý bẫy: video lớn làm nghẽn mạng, đứt khi gập máy
- **Không treo mạng nhà trọ:**
  - Giới hạn tốc độ tải lên/tải xuống trong phần cài đặt mạng của ứng dụng.
  - Đặt lịch tải video lớn vào ban đêm hoặc giờ ít người dùng mạng.
  - Chỉ **một máy** tải video gốc lên, các máy khác dùng On-Demand.
- **Không đứt khi gập máy:**
  - Cắm sạc và tắt chế độ ngủ khi đang tải lên (Mac: System Settings → Battery/Power Adapter → chặn ngủ khi nối nguồn).
  - Chia video thành các file nhỏ hơn hoặc tải theo từng đợt.
  - Ứng dụng đồng bộ tự **tiếp tục** từ chỗ dừng khi có mạng/máy bật lại, nên không phải tải lại từ đầu.

## Phần 2: Báo cáo dung lượng

Giả định minh họa: mỗi người mở cùng lúc khoảng 2 video, mỗi video 5GB.

| Chỉ số | Mirror (tải toàn bộ) | Files On-Demand |
|---|---|---|
| Dung lượng Cloud | 500GB | 500GB |
| Dung lượng chiếm trên SSD | 500GB | ≈ 2 × 5 = **10GB** (+ vài MB bản giữ chỗ) |
| So với SSD 256GB | 500 / 256 ≈ **195%** (tràn, thiếu 244GB) | 10 / 256 ≈ **3,9%** |
| Dung lượng trống còn lại | Không đủ | 256 − 10 = **246GB** |

**Chứng minh hiệu quả:**
- Cloud lớn hơn SSD khoảng 500 / 256 ≈ **1,95 lần**, Mirror không thể chạy.
- Với On-Demand, dung lượng chiếm trên máy phụ thuộc vào **số file đang mở**, không phụ thuộc tổng dung lượng Cloud.
- Vì vậy Cloud tăng lên 1TB hay hơn nữa, SSD vẫn chỉ tốn đúng phần file đang dùng.

## Phần 3: Quản lý vòng đời dữ liệu
- Video đang dùng: để trên Cloud, tải khi cần, xong thì Free up space.
- Video quan trọng: đặt tên rõ, giữ trong thư mục riêng, rà soát định kỳ.
- Video không còn cần: xóa hoặc chuyển sang lưu trữ lạnh để giảm dung lượng Cloud.