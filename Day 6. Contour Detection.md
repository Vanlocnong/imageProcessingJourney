# Day 6 Contour Detection

### 1.cv2.findContours()

Bạn đang tìm hiểu về hàm `cv2.findContours()` trong OpenCV và muốn so sánh nó với `cv2.Canny()`. Dưới đây là giải thích chi tiết từng hàm, cách sử dụng và sự khác biệt giữa chúng.
---
## **1. Hàm `cv2.findContours()`**
Hàm này dùng để **tìm đường viền (contours)** của các đối tượng trong ảnh nhị phân (binary image). Contours là các đường cong khép kín bao quanh các đối tượng trong ảnh.

### **Cú pháp**
```python
contours, hierarchy = cv2.findContours(image, mode, method[, contours[, hierarchy[, offset]]])
```

### **Giải thích tham số**
| Tham số | Kiểu dữ liệu | Mô tả |
|---------|-------------|-------|
| **`image`** | `numpy.ndarray` (ảnh nhị phân) | Ảnh đầu vào **phải là ảnh nhị phân** (thường được xử lý trước bằng `cv2.threshold()` hoặc `cv2.Canny()`). |
| **`mode`** | `int` | Phương pháp lấy contours:<br>- `cv2.RETR_EXTERNAL`: Chỉ lấy contours ngoài cùng.<br>- `cv2.RETR_LIST`: Lấy tất cả contours, không phân cấp.<br>- `cv2.RETR_TREE`: Lấy tất cả contours và xây dựng cây phân cấp. |
| **`method`** | `int` | Phương pháp xấp xỉ contour:<br>- `cv2.CHAIN_APPROX_NONE`: Lưu tất cả điểm biên.<br>- `cv2.CHAIN_APPROX_SIMPLE`: Nén các đoạn thẳng thành 2 điểm đầu-cuối (tiết kiệm bộ nhớ). |
| **`contours`** | `list` | **Output**: Danh sách các contours (mỗi contour là một mảng NumPy chứa tọa độ điểm). |
| **`hierarchy`** | `numpy.ndarray` | **Output**: Mảng chứa thông tin phân cấp giữa các contours (dùng khi `mode=RETR_TREE`). |

### **Ví dụ sử dụng**
```python
import cv2

# Đọc ảnh và chuyển sang grayscale
img = cv2.imread('object.jpg', cv2.IMREAD_GRAYSCALE)

# Nhị phân hóa ảnh
ret, binary_img = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Tìm contours
contours, hierarchy = cv2.findContours(binary_img, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Vẽ contours lên ảnh gốc (màu đỏ, độ dày 2)
cv2.drawContours(img, contours, -1, (0, 0, 255), 2)

cv2.imshow('Contours', img)
cv2.waitKey(0)
```

---

## **2. Hàm `cv2.Canny()`**
Hàm này dùng để **phát hiện biên cạnh (edge detection)** dựa trên thuật toán Canny. Khác với `findContours()`, `Canny()` trả về ảnh nhị phân chỉ chứa các pixel biên.

### **Cú pháp**
```python
edges = cv2.Canny(image, threshold1, threshold2[, edges[, apertureSize[, L2gradient]]])
```

### **Giải thích tham số**
| Tham số | Kiểu dữ liệu | Mô tả |
|---------|-------------|-------|
| **`image`** | `numpy.ndarray` (grayscale) | Ảnh đầu vào (phải là ảnh grayscale). |
| **`threshold1`** | `int` | Ngưỡng dưới (các cạnh yếu hơn bị loại bỏ). |
| **`threshold2`** | `int` | Ngưỡng trên (các cạnh mạnh hơn được giữ lại). |
| **`edges`** | `numpy.ndarray` | **Output**: Ảnh nhị phân chứa các đường biên (giá trị 255 là biên, 0 là nền). |

### **Ví dụ sử dụng**
```python
import cv2

# Đọc ảnh và chuyển sang grayscale
img = cv2.imread('object.jpg', cv2.IMREAD_GRAYSCALE)

# Phát hiện biên Canny
edges = cv2.Canny(img, 100, 200)  # Ngưỡng dưới=100, ngưỡng trên=200

cv2.imshow('Canny Edges', edges)
cv2.waitKey(0)
```

---

## **3. So sánh `cv2.findContours()` và `cv2.Canny()`**
| Tiêu chí | `cv2.findContours()` | `cv2.Canny()` |
|----------|----------------------|---------------|
| **Mục đích** | Tìm đường bao (contours) của đối tượng | Phát hiện biên cạnh (edges) |
| **Đầu vào** | Ảnh nhị phân (binary image) | Ảnh grayscale |
| **Đầu ra** | Danh sách contours (tập hợp điểm) | Ảnh nhị phân chứa biên |
| **Ứng dụng** | Nhận dạng hình dạng, đếm đối tượng | Phát hiện cạnh, tiền xử lý trước khi tìm contours |
| **Thường dùng kết hợp** | Sau khi dùng `threshold()` hoặc `Canny()` | Trước khi dùng `findContours()` |

### **Khi nào dùng hàm nào?**
- **Dùng `Canny()`** khi bạn cần phát hiện **các cạnh chi tiết** trong ảnh (ví dụ: phát hiện góc, đường thẳng).
- **Dùng `findContours()`** khi bạn muốn **phân tích hình dạng đối tượng** (ví dụ: đếm số vật thể, đo kích thước).

### **Ví dụ kết hợp cả hai hàm**
```python
import cv2

img = cv2.imread('object.jpg', cv2.IMREAD_GRAYSCALE)

# Bước 1: Phát hiện biên bằng Canny
edges = cv2.Canny(img, 100, 200)

# Bước 2: Tìm contours từ ảnh biên
contours, hierarchy = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Vẽ contours lên ảnh gốc
result = cv2.cvtColor(img, cv2.COLOR_GRAY2BGR)  # Chuyển sang ảnh màu để vẽ contour màu đỏ
cv2.drawContours(result, contours, -1, (0, 0, 255), 2)

cv2.imshow('Combined Result', result)
cv2.waitKey(0)
```

---

## **4. Kết luận**
- **`cv2.findContours()`** → Tìm **đường bao** (contours) của đối tượng từ ảnh nhị phân.
- **`cv2.Canny()`** → Tạo **ảnh biên** (edges) từ ảnh grayscale, thường dùng làm đầu vào cho `findContours()`.
- **Kết hợp cả hai** sẽ giúp phát hiện và phân tích đối tượng chính xác hơn.

Hy vọng giải thích này giúp bạn hiểu rõ và áp dụng đúng hai hàm quan trọng này trong OpenCV! 🚀

#### Note : giải thích chi tiết về hàm cv2.threshold

Hàm `cv2.threshold()` trong OpenCV là một hàm quan trọng dùng để áp dụng ngưỡng (thresholding) lên một ảnh grayscale. Mục đích là để phân loại pixel thành các nhóm dựa trên giá trị ngưỡng được chỉ định. Dưới đây là giải thích chi tiết về các tham số đầu vào (input) và đầu ra (output) của hàm:

---

### **Cú pháp**
```python
retval, dst = cv2.threshold(src, thresh, maxval, type[, dst])
```

---

### **Giải thích các tham số**

#### **1. Tham số đầu vào (Input Parameters)**
| Tham số | Kiểu dữ liệu | Giải thích chi tiết |
|---------|-------------|---------------------|
| **`src`** | `numpy.ndarray` (ảnh grayscale) | Ảnh đầu vào (phải là ảnh grayscale, 8-bit hoặc 32-bit float). |
| **`thresh`** | `float` | Giá trị ngưỡng (threshold value) dùng để phân loại pixel. |
| **`maxval`** | `float` | Giá trị gán cho pixel nếu pixel đó vượt ngưỡng (dùng trong một số phương pháp thresholding như `THRESH_BINARY`, `THRESH_BINARY_INV`). |
| **`type`** | `int` | Loại ngưỡng (thresholding type), quyết định cách áp dụng ngưỡng. OpenCV cung cấp các loại sau:<br>- `cv2.THRESH_BINARY`<br>- `cv2.THRESH_BINARY_INV`<br>- `cv2.THRESH_TRUNC`<br>- `cv2.THRESH_TOZERO`<br>- `cv2.THRESH_TOZERO_INV`<br>- `cv2.THRESH_OTSU` (thường kết hợp với các loại khác)<br>- `cv2.THRESH_TRIANGLE` (tự động chọn ngưỡng) |

#### **2. Tham số đầu ra (Output Parameters)**
| Tham số | Kiểu dữ liệu | Giải thích chi tiết |
|---------|-------------|---------------------|
| **`retval`** | `float` | Giá trị ngưỡng được sử dụng (đặc biệt hữu ích khi dùng `THRESH_OTSU` hoặc `THRESH_TRIANGLE`, vì OpenCV tự động tính toán ngưỡng tối ưu). |
| **`dst`** | `numpy.ndarray` | Ảnh kết quả sau khi áp dụng ngưỡng (cùng kích thước và kiểu dữ liệu với `src`). |

---

### 2.Vậy có dùng ảnh đầu vào cho hàm cv2.findContours() được không ? Tại sao ?

### **Câu trả lời:**
**Có**, bạn **có thể dùng ảnh đầu ra từ `cv2.Canny()` làm đầu vào cho `cv2.findContours()`**, nhưng **không nên dùng trực tiếp** vì ảnh từ `Canny` thường chứa nhiều nhiễu và đường biên không liên tục. Thay vào đó, nên kết hợp **xử lý ảnh nhị phân (thresholding) trước** để đảm bảo contours được tìm chính xác.

---

## **1. Tại sao có thể dùng ảnh từ `cv2.Canny()` cho `cv2.findContours()`?**
- **Lý do:**  
  - `cv2.Canny()` trả về **ảnh nhị phân** (chỉ có 2 giá trị: `0` và `255`), đúng định dạng đầu vào của `cv2.findContours()` (yêu cầu ảnh nhị phân).
  - Về mặt kỹ thuật, OpenCV không báo lỗi nếu bạn truyền ảnh Canny vào `findContours()`.

- **Ví dụ chạy được:**
  ```python
  edges = cv2.Canny(img, 100, 200)
  contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)  # Không lỗi
  ```

---

## **2. Tại sao không nên dùng trực tiếp ảnh Canny?**
### **Vấn đề gặp phải:**
1. **Nhiễu và biên đứt đoạn**  
   - Ảnh Canny thường chứa nhiều **nhiễu** (cạnh giả) và **đường biên không liên tục** → `findContours()` sẽ tìm ra nhiều contours rời rạc, không khép kín.
   - Ví dụ: Một hình chữ nhật trong ảnh Canny có thể bị đứt thành 4 đoạn thẳng riêng biệt thay vì 1 contour khép kín.

2. **Contours không chính xác**  
   - `findContours()` hoạt động tốt nhất khi đối tượng có **đường viền liền mạch**. Nếu ảnh Canny có biên mỏng/đứt, kết quả sẽ kém ổn định.

3. **Khó kiểm soát ngưỡng**  
   - Canny sử dụng 2 ngưỡng (`threshold1`, `threshold2`), việc chọn sai ngưỡng có thể làm mất biên quan trọng hoặc tạo nhiều biên thừa.

---

## **3. Giải pháp tốt hơn: Kết hợp Thresholding + Canny**
Để có contours chính xác, nên:
1. **Tiền xử lý ảnh** (Làm mờ, giảm nhiễu) → Dùng `cv2.GaussianBlur()`.
2. **Áp dụng thresholding** (nhị phân hóa) → Dùng `cv2.threshold()` hoặc `cv2.adaptiveThreshold()`.
3. **Dùng Canny (nếu cần)** để làm rõ biên.
4. **Tìm contours** từ ảnh nhị phân sạch.

### **Ví dụ tối ưu:**
```python
import cv2

# Đọc ảnh và chuyển sang grayscale
img = cv2.imread('object.jpg', cv2.IMREAD_GRAYSCALE)

# Bước 1: Làm mờ ảnh để giảm nhiễu
blurred = cv2.GaussianBlur(img, (5, 5), 0)

# Bước 2: Nhị phân hóa ảnh (Otsu tự động chọn ngưỡng)
ret, binary = cv2.threshold(blurred, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)

# Bước 3 (Tùy chọn): Dùng Canny để làm rõ biên
edges = cv2.Canny(binary, 50, 150)

# Bước 4: Tìm contours từ ảnh nhị phân (hoặc ảnh Canny đã xử lý)
contours, _ = cv2.findContours(binary, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Vẽ contours lên ảnh gốc
result = cv2.cvtColor(img, cv2.COLOR_GRAY2BGR)
cv2.drawContours(result, contours, -1, (0, 255, 0), 2)

cv2.imshow('Optimized Contours', result)
cv2.waitKey(0)
```

---

## **4. Khi nào nên dùng ảnh Canny làm đầu vào?**
Chỉ dùng trực tiếp ảnh Canny nếu:
- Bạn **chắc chắn** ảnh Canny có **biên liên tục, ít nhiễu** (ví dụ: ảnh đơn giản, nền đồng nhất).
- Bạn muốn **phát hiện các cạnh rời rạc** (không cần contours khép kín).

---

## **5. Kết luận**
| Trường hợp | Nên làm |
|------------|---------|
| **Dùng trực tiếp ảnh Canny** | Không khuyến khích (trừ khi biên rất sạch). |
| **Kết hợp Thresholding + Canny** | Cách tốt nhất để có contours chính xác. |
| **Chỉ dùng Thresholding** | Đủ nếu ảnh có độ tương phản cao. |

👉 **Lời khuyên:** Luôn **thử nghiệm cả 2 cách** (chỉ thresholding hoặc kết hợp Canny) để chọn phương án tối ưu cho bài toán cụ thể của bạn!

### **Các loại ngưỡng (Thresholding Types)**
Giả sử:
- \( \text{src}(x,y) \): Giá trị pixel tại vị trí \((x, y)\).
- \( \text{thresh} \): Giá trị ngưỡng.
- \( \text{maxval} \): Giá trị tối đa (thường 255 với ảnh 8-bit).

| Loại ngưỡng | Công thức | Mô tả |
|-------------|-----------|-------|
| **`cv2.THRESH_BINARY`** | \( \text{dst}(x,y) = \begin{cases} \text{maxval} & \text{if } \text{src}(x,y) > \text{thresh} \\ 0 & \text{otherwise} \end{cases} \) | Pixel > ngưỡng → `maxval`, ngược lại → `0`. |
| **`cv2.THRESH_BINARY_INV`** | \( \text{dst}(x,y) = \begin{cases} 0 & \text{if } \text{src}(x,y) > \text{thresh} \\ \text{maxval} & \text{otherwise} \end{cases} \) | Ngược lại với `THRESH_BINARY`. |
| **`cv2.THRESH_TRUNC`** | \( \text{dst}(x,y) = \begin{cases} \text{thresh} & \text{if } \text{src}(x,y) > \text{thresh} \\ \text{src}(x,y) & \text{otherwise} \end{cases} \) | Pixel > ngưỡng → gán bằng `thresh`, giữ nguyên giá trị cũ nếu ≤ ngưỡng. |
| **`cv2.THRESH_TOZERO`** | \( \text{dst}(x,y) = \begin{cases} \text{src}(x,y) & \text{if } \text{src}(x,y) > \text{thresh} \\ 0 & \text{otherwise} \end{cases} \) | Pixel ≤ ngưỡng → `0`, giữ nguyên nếu > ngưỡng. |
| **`cv2.THRESH_TOZERO_INV`** | \( \text{dst}(x,y) = \begin{cases} 0 & \text{if } \text{src}(x,y) > \text{thresh} \\ \text{src}(x,y) & \text{otherwise} \end{cases} \) | Ngược lại với `THRESH_TOZERO`. |
| **`cv2.THRESH_OTSU`** | Kết hợp với các loại khác (ví dụ: `cv2.THRESH_BINARY \| cv2.THRESH_OTSU`) | Tự động tính toán ngưỡng tối ưu dựa trên thuật toán Otsu (phân tích histogram). |
| **`cv2.THRESH_TRIANGLE`** | Tương tự Otsu | Tự động chọn ngưỡng dựa trên thuật toán Triangle (phù hợp với ảnh có histogram 1 peak rõ ràng). |

---

### **Ví dụ minh họa**
```python
import cv2
import numpy as np

# Đọc ảnh grayscale
img = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)

# Áp dụng threshold nhị phân
ret, thresh_binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Áp dụng Otsu's thresholding
ret_otsu, thresh_otsu = cv2.threshold(img, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)

print("Ngưỡng Otsu tính được:", ret_otsu)
```

- **`THRESH_BINARY`**: Pixel > 127 → 255 (trắng), ngược lại → 0 (đen).
- **`THRESH_OTSU`**: OpenCV tự tính ngưỡng tối ưu (giá trị trả về trong `ret_otsu`).

---

### **Lưu ý quan trọng**
1. Ảnh đầu vào **phải là ảnh grayscale**.
2. Nếu dùng `THRESH_OTSU` hoặc `THRESH_TRIANGLE`, giá trị `thresh` truyền vào bị bỏ qua (có thể đặt `0`), vì OpenCV tự tính ngưỡng.
3. Ảnh kết quả (`dst`) là ảnh nhị phân nếu dùng `THRESH_BINARY`, `THRESH_BINARY_INV`.


