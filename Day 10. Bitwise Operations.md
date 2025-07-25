Dưới đây là bài giảng chi tiết về **các phép toán bitwise trong OpenCV**, bao gồm lý thuyết, ứng dụng và ví dụ minh họa bằng Python:

---

### **1. Giới thiệu về phép toán bitwise**
Các phép toán bitwise thao tác trực tiếp trên các bit (0 và 1) của dữ liệu ảnh. Trong OpenCV, chúng thường dùng với ảnh nhị phân (binary images) hoặc mặt nạ (masks). 4 phép toán chính:
- `AND` (`cv2.bitwise_and`)
- `OR` (`cv2.bitwise_or`)
- `NOT` (`cv2.bitwise_not`)
- `XOR` (`cv2.bitwise_xor`)

---

### **2. Cách hoạt động chi tiết**
Giả sử điểm ảnh (pixel) được biểu diễn dưới dạng số nguyên 8-bit (giá trị từ 0-255).

#### **Ví dụ với hai pixel:**
- Pixel A: `150` → Nhị phân: `10010110`
- Pixel B: `75`  → Nhị phân: `01001011`

| Phép toán | Kết quả nhị phân | Kết quả thập phân | Công thức OpenCV |
|-----------|------------------|-------------------|------------------|
| **AND**   | `00000010`       | `2`               | `cv2.bitwise_and(A, B)` |
| **OR**    | `11011111`       | `223`             | `cv2.bitwise_or(A, B)`  |
| **XOR**   | `11011101`       | `221`             | `cv2.bitwise_xor(A, B)` |
| **NOT A** | `01101001`       | `105`             | `cv2.bitwise_not(A)`    |

---

### **3. Tham số quan trọng trong OpenCV**
Các hàm nhận 3 tham số chính:
```python
cv2.bitwise_operation(src1, src2, dst=None, mask=None)
```
- `src1`, `src2`: Ảnh đầu vào (cùng kích thước và định dạng).
- `mask` (tùy chọn): Vùng áp dụng phép toán (chỉ thực hiện tại nơi mask ≠ 0).

---

### **4. Ứng dụng thực tế**

#### **a. Tạo mặt nạ (Masking)**
Trích xuất đối tượng từ ảnh gốc bằng mặt nạ nhị phân:
```python
import cv2
import numpy as np

# Đọc ảnh và tạo mask
image = cv2.imread('image.jpg')
mask = cv2.imread('mask.png', 0)  # Ảnh grayscale

# Áp dụng mask: chỉ giữ lại phần "AND" với mask
result = cv2.bitwise_and(image, image, mask=mask)
```

#### **b. Kết hợp ảnh**
Ghép các phần của 2 ảnh:
```python
# Tạo hình chữ nhật và hình tròn
rect = np.zeros((300, 300), dtype="uint8")
cv2.rectangle(rect, (50, 50), (250, 250), 255, -1)

circle = np.zeros((300, 300), dtype="uint8")
cv2.circle(circle, (150, 150), 150, 255, -1)

# Kết hợp: Hình mặt trăng lưỡi liềm (XOR)
crescent = cv2.bitwise_xor(rect, circle)
```

#### **c. Loại bỏ nền**
Xóa nền trắng khỏi logo:
```python
logo = cv2.imread('logo_white_bg.jpg')
gray = cv2.cvtColor(logo, cv2.COLOR_BGR2GRAY)

# Tạo mask: chuyển nền trắng thành đen
_, mask_inv = cv2.threshold(gray, 220, 255, cv2.THRESH_BINARY_INV)

# Áp dụng để lấy logo không nền
result = cv2.bitwise_and(logo, logo, mask=mask_inv)
```

---

### **5. Demo đầy đủ với OpenCV**
```python
import cv2
import numpy as np

# Tạo ảnh đen kích thước 300x300
img = np.zeros((300, 300, 3), dtype="uint8")

# Vẽ hình chữ nhật màu trắng
rectangle = cv2.rectangle(img.copy(), (50, 50), (250, 250), (255, 255, 255), -1)

# Vẽ hình tròn màu trắng
circle = cv2.circle(img.copy(), (150, 150), 150, (255, 255, 255), -1)

# Tính toán các phép toán
bitwise_and = cv2.bitwise_and(rectangle, circle)
bitwise_or = cv2.bitwise_or(rectangle, circle)
bitwise_xor = cv2.bitwise_xor(rectangle, circle)
bitwise_not = cv2.bitwise_not(rectangle)

# Hiển thị kết quả
cv2.imshow("AND: Giao nhau", bitwise_and)
cv2.imshow("OR: Hợp", bitwise_or)
cv2.imshow("XOR: Loại trừ", bitwise_xor)
cv2.imshow("NOT: Đảo bit", bitwise_not)
cv2.waitKey(0)
```

**Kết quả:**
- `AND`: Vùng giao nhau giữa hình chữ nhật và hình tròn.
- `OR`: Toàn bộ diện tích bao phủ bởi cả hai hình.
- `XOR`: Phần chỉ thuộc một trong hai hình (hình lưỡi liềm).
- `NOT`: Đảo ngược màu sắc (hình chữ nhật đen trên nền trắng).

---

### **6. Lưu ý quan trọng**
- Ảnh đầu vào **phải cùng kích thước và định dạng**.
- Sử dụng **mask** để giới hạn vùng tác động.
- Phép toán thực hiện trên **từng kênh màu riêng biệt** (BGR).
- Luôn chuyển ảnh mask về **grayscale** (1 kênh) khi dùng trong tham số `mask`.

---

### **7. Ứng dụng nâng cao**
- **Xử lý ROI (Region of Interest)**: Kết hợp `bitwise_and` với mask để xử lý từng vùng ảnh.
- **Watermarking**: Nhúng logo vào ảnh bằng phép `OR`/`XOR`.
- **Augmented Reality**: Thay thế nền xanh (green screen) sử dụng `bitwise_and` với mask đảo.

Hiểu rõ các phép toán bitwise giúp bạn linh hoạt trong việc xử lý ảnh nhị phân, tạo mặt nạ và kết hợp đối tượng!