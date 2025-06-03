# Day 4. Essential Functions

### 1.Converting to gray:

    img_src = (path)
    gray = cv2.cvtColor( mg_src , cv2.COLOR_BGR2GRAY)

### 2.Blur:
    Gaussian Blur là một kỹ thuật làm mờ ảnh phổ biến trong xử lý ảnh, được sử dụng để giảm nhiễu và làm mịn hình ảnh. Trong OpenCV, Gaussian Blur được thực hiện bằng hàm `cv2.GaussianBlur()`, giúp làm mờ ảnh bằng cách áp dụng bộ lọc Gaussian.
    Kỹ thuật này hoạt động bằng cách tính toán giá trị trung bình có trọng số của các pixel xung quanh một điểm nhất định, sử dụng hàm Gaussian để xác định mức độ ảnh hưởng của từng pixel. Điều này giúp loại bỏ nhiễu và các chi tiết không cần thiết, tạo ra một hiệu ứng làm mờ tự nhiên.

> cv2.GaussianBlur(src, ksize, sigmaX, dst=None, sigmaY=None, borderType=None)
    - `src`: Ảnh nguồn.
        
    - `ksize`: Kích thước kernel (phải là số lẻ, ví dụ: `(3,3)`, `(5,5)`).
        
    - `sigmaX`: Độ lệch chuẩn theo hướng X.
        
    - `sigmaY`: Độ lệch chuẩn theo hướng Y (nếu không cung cấp, mặc định bằng `sigmaX`).
        
    - `borderType`: Kiểu biên (mặc định là `cv2.BORDER_DEFAULT`).


### 3.Edge cascade:
    Sử dụng thuật toán **Canny Edge Detection** để phát hiện cạnh trong ảnh. Đây là một phương pháp phổ biến trong xử lý ảnh, giúp xác định các đường biên rõ ràng bằng cách loại bỏ nhiễu và tìm các điểm có sự thay đổi mạnh về cường độ sáng.

    - `cv.Canny()`: Đây là hàm trong OpenCV dùng để phát hiện cạnh bằng thuật toán Canny.
        
    - `blur_img`: Ảnh đầu vào đã được làm mờ trước đó (thường bằng Gaussian Blur) để giảm nhiễu.
        
    - `125, 175`: Hai giá trị ngưỡng (**threshold**):
    
      - **125**: Ngưỡng dưới – các pixel có giá trị gradient thấp hơn sẽ bị loại bỏ.
          
      - **175**: Ngưỡng trên – các pixel có giá trị gradient cao hơn sẽ được giữ lại làm cạnh.
          
      - Các pixel có giá trị gradient nằm giữa hai ngưỡng sẽ được kiểm tra thêm dựa trên sự liên kết với các pixel cạnh mạnh.
      - 
    img_src = (path)
    blur = cv2.GaussianBlur(img_src , (5,5) , cv2.BORDER_DEFAULT)
    canny = cv2.Canny(blur ,  125 , 175 ,)

### 4.Dilating the image:

#### Ứng dụng của **Dilate**:
    - **Làm dày chữ viết tay** trong nhận dạng ký tự.    
    - **Kết nối các đường nét bị đứt gãy** trong ảnh nhị phân.   
    - **Loại bỏ nhiễu nhỏ** bằng cách mở rộng vùng sáng.
    - 
    canny = cv2.Canny(blur , 125 , 175)
    dilated = cv2.dilate(canny  , (5,5) , interations = 3)
    cv.imshow("Dilate",dilated)

### 5.Eroding:
    Trong OpenCV, **Erosion** (xói mòn) là một kỹ thuật xử lý ảnh thuộc nhóm **biến đổi hình thái học (Morphological Transformations)**. Nó được sử dụng để **thu nhỏ** các vùng sáng trong ảnh, giúp loại bỏ nhiễu và làm mịn các đường viền2.

### 🔹 Cách hoạt động của **Erosion**:

    - **Loại bỏ pixel ở biên của đối tượng sáng** trong ảnh.  
    - **Làm mỏng** các đường nét hoặc vùng sáng.
    - **Loại bỏ nhiễu nhỏ** bằng cách thu nhỏ vùng sáng.  

### 🔹 Công thức:

    Erosion sử dụng một **kernel** (ma trận nhỏ) để quét qua ảnh. Giá trị của mỗi pixel được thay thế bằng **giá trị nhỏ nhất** của các pixel xung quanh nó trong phạm vi kernel

    eroded = cv.erode(canny , (5,5) , iterations=1)
    cv.imshow("Eroded" , eroded)


### 6.Image Crop:

    img = cv2.imread(path)
    cropped = img[100:200 , 300:100]