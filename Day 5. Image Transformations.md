# Day 5. Image Transformations:

### 1 Translate:

##### Translate function:
    def translate(img , x , y):
        transMat = np.float32([[1,0,x] , [0,1,y]])
        dimensions = (img.shape[1] , img.shape[0])
        return cv.warpAffine(img , transMat , dimensions)

- -x --> left
- -y --> up
- x --> right
- y --> down

  
##### Detail:
    translated = translate(img , 30 , 50)
    cv.imshow("Translated Image" , translated)
    `transMat = np.float32([[1,0,x], [0,1,y]])`
  - Đây là **ma trận biến đổi Affine** dùng để dịch chuyển ảnh.
  - `[[1,0,x], [0,1,y]]` là **ma trận dịch chuyển**, trong đó:
      - `1,0,x`: Dịch chuyển theo **trục X** (x pixel). 
      - `0,1,y`: Dịch chuyển theo **trục Y** (y pixel).   
  - Nếu `x > 0`, ảnh sẽ **dịch sang phải**; nếu `x < 0`, ảnh sẽ **dịch sang trái**.  
  - Nếu `y > 0`, ảnh sẽ **dịch xuống dưới**; nếu `y < 0`, ảnh sẽ **dịch lên trên**.
    

2️⃣ `dimensions = (img.shape[1], img.shape[0])`
  - Xác định **kích thước ảnh đầu ra**.
  - `img.shape[1]`: Chiều rộng ảnh. 
  - `img.shape[0]`: Chiều cao ảnh.  
  - Điều này đảm bảo ảnh sau khi dịch chuyển vẫn giữ nguyên kích thước ban đầu.
    

3️⃣ `cv.warpAffine(img, transMat, dimensions)`
  - Hàm `cv.warpAffine()` áp dụng **ma trận biến đổi Affine** lên ảnh.
  - `img`: Ảnh gốc. 
  - `transMat`: Ma trận dịch chuyển.   
  - `dimensions`: Kích thước ảnh đầu ra.   
  - Kết quả là ảnh đã được **dịch chuyển** theo hướng `x` và `y` và giữ nguyên kích thước



##### ROTATION:

  1. Khởi tạo hàm:
  def rotation(img , angle , rotPoint = None):
  - Đây là một hàm Python nhận ba tham số:
      - `img`: Ảnh đầu vào cần xoay.
      - `angle`: Góc xoay (đơn vị độ).
      - `rotPoint`: Điểm xoay, nếu không được cung cấp, mặc định là tâm ảnh.
          
  2. Lấy kích thước ảnh:
  (height , width) = img.shape[:2]
  - `img.shape[:2]` lấy **chiều cao** và **chiều rộng** của ảnh.
  - `shape` của một ảnh thường có ba giá trị `(height, width, channels)`, nhưng ta chỉ lấy 2 giá trị đầu tiên.
  3. Xác định điểm xoay:
  if rotPoint is None:
      rotPoint = (width//2 , height//2)
  - Nếu `rotPoint` không được truyền vào, ta lấy **tâm ảnh** làm điểm xoay:      
      - `width//2`: Tọa độ x của điểm giữa ảnh.          
      - `height//2`: Tọa độ y của điểm giữa ảnh.    
      -   
  4. Tạo ma trận xoay:
  rotMat = cv.getRotationMatrix2D(rotPoint , angle , 1.0)
  - `cv.getRotationMatrix2D(center, angle, scale)`:
      - `center`: Tọa độ tâm xoay.
      - `angle`: Góc xoay (ở đây là -30 độ, tức xoay ngược chiều kim đồng hồ 30 độ).
      - `scale`: Hệ số tỷ lệ ảnh (1.0 nghĩa là giữ nguyên kích thước).
      - 
  5. Xác định kích thước đầu ra:
  dimensions = (width,height)
  - `dimensions`: Giữ nguyên kích thước ảnh gốc để tránh bị cắt mất phần hình ảnh.
  - 
  6. Áp dụng biến đổi xoay:
  return cv.warpAffine(img , rotMat , dimensions)
  - `cv.warpAffine(img, M, dsize)`:
      - `img`: Ảnh cần biến đổi.
      - `M`: Ma trận biến đổi (ở đây là `rotMat`).
      - `dsize`: Kích thước ảnh đầu ra.

  Chạy và hiển thị hình ảnh:

  rotationImage = rotation(img , -30)
  cv.imshow("Rotated Image" , rotationImage)
  - Gọi hàm `rotation()` với góc xoay `-30 độ`.
  - Hiển thị ảnh xoay bằng `cv.imshow()`.
