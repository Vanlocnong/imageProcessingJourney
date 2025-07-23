# Day 7 Color space
> Không gian màu trong OpenCV được quy ước là BGR, thay vì các môi trường khacslaf RGB.

> Chuyển đổi giữa các không gian màu BGR -> RGB, BGR -> LAB, BGR -> HSV, BG -> GRAY SCALE.

## Thư viện matplotlib:

### **Matplotlib trong Python là gì?**
**Matplotlib** là một thư viện mã nguồn mở mạnh mẽ dùng để **trực quan hóa dữ liệu** trong Python. Nó được thiết kế để tạo các biểu đồ, đồ thị chất lượng cao từ dữ liệu, với giao diện linh hoạt và dễ sử dụng. Matplotlib được xây dựng dựa trên **NumPy** và tích hợp tốt với hệ sinh thái khoa học dữ liệu Python (Pandas, SciPy, scikit-learn...).

---

### **Matplotlib dùng để làm gì?**
Matplotlib được sử dụng rộng rãi để **biểu diễn dữ liệu dưới dạng hình ảnh** giúp phân tích, trình bày kết quả. Dưới đây là những ứng dụng chính:

1. **Vẽ đa dạng loại biểu đồ**:
   - **Đồ thị đường** (`line plot`): Hiển thị xu hướng dữ liệu theo thời gian.
   - **Biểu đồ cột** (`bar chart`): So sánh giá trị giữa các nhóm.
   - **Biểu đồ phân tán** (`scatter plot`): Thể hiện mối quan hệ giữa 2 biến.
   - **Biểu đồ tròn** (`pie chart`): Tỷ lệ phần trăm của các thành phần.
   - **Histogram**: Phân bố tần suất của dữ liệu.
   - **Box plot**: Tóm tắt phân phối dữ liệu (median, outlier...).
   - **Đồ thị 3D**: Trực quan hóa dữ liệu đa chiều.

2. **Tuỳ chỉnh chi tiết**:
   - Thay đổi **màu sắc**, **kiểu đường**, **độ dày**.
   - Thêm **tiêu đề**, **nhãn trục**, **chú thích** (legend), **công thức toán học** (LaTeX).
   - Điều chỉnh **tỷ lệ trục**, **giới hạn hiển thị**, **lưới** (grid).

3. **Xuất bản và chia sẻ**:
   - Lưu biểu đồ dưới nhiều định dạng: **PNG**, **JPG**, **PDF**, **SVG**.
   - Nhúng vào ứng dụng web (dùng `WebAgg` backend) hoặc hiển thị trong Jupyter Notebook.

4. **Tích hợp với các thư viện khác**:
   - **Pandas**: Vẽ trực tiếp từ DataFrame.
   - **Seaborn**: Dựa trên Matplotlib để tạo biểu đồ phức tạp với ít code hơn.
   - **Plotly**: Kết hợp để tạo biểu đồ tương tác.

---

### **Ví dụ minh họa (vẽ đồ thị đường đơn giản)**
```python
import matplotlib.pyplot as plt
import numpy as np

# Tạo dữ liệu mẫu
x = np.linspace(0, 10, 100)  # 100 điểm từ 0 đến 10
y = np.sin(x)  # Giá trị sin(x)

# Vẽ đồ thị
plt.figure(figsize=(8, 4))  # Kích thước hình
plt.plot(x, y, label='sin(x)', color='blue', linewidth=2) 
plt.title("Đồ thị hàm sin(x)")  # Tiêu đề
plt.xlabel("x")  # Nhãn trục x
plt.ylabel("y")  # Nhãn trục y
plt.grid(True)  # Hiện lưới
plt.legend()  # Hiện chú thích

# Hiển thị biểu đồ
plt.show()
```

**Kết quả**:  
![sin(x) plot](https://i.imgur.com/Yn4tG3m.png)

---

### **Tại sao nên dùng Matplotlib?**
- **Linh hoạt**: Kiểm soát gần như mọi chi tiết trên biểu đồ.
- **Phổ biến**: Tiêu chuẩn de facto trong cộng đồng khoa học dữ liệu Python.
- **Dễ học**: Cú pháp rõ ràng, tài liệu phong phú, ví dụ đa dạng.

> 💡 **Mẹo**: Khi làm việc nhanh trong Jupyter Notebook, hãy dùng magic command `%matplotlib inline` để hiển thị biểu đồ ngay trong notebook.