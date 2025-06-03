# Day 1. Install Librarys & reading imag and video

- install open cv mở rộng : pip install opencv-contrib-python
- install thư viện **Caer** : pip install caer

#### Sau khi cài đặt, bạn có thể thử kiểm tra bằng cách nhập:
    import caer
    print(caer.__version__)
>Caer:
>thư viện chuyên về xử lý ảnh (image processing) và trí tuệ nhân tạo (AI), giúp bạn dễ dàng thao >tác với hình ảnh, làm sạch dữ liệu, và áp dụng các mô hình thị giác máy tính.

#### Các tính năng chính của Caer**:
- Hỗ trợ chuyển đổi hình ảnh thành định dạng NumPy dễ dàng.
- Cung cấp các phương pháp xử lý ảnh, như thay đổi kích thước, xoay, và điều chỉnh màu sắc.
- Tích hợp các thuật toán học sâu và thị giác máy tính.   
- Dễ sử dụng, tối ưu hiệu suất khi thao tác với dữ liệu ảnh.

## 1.Reading image and video:

##### 1.1.Reading image:

    import cv2 as cv
    img = cv.imread(path)
    cv.imshow(img)
    cv.waitkey(0)

##### 1.2.reading video:
    import cv2 as cv
    capture = cv.VideoCapture(path)
    while True:
        isTrue , frame = capture.read()
        cv.imshow(frame)
        if cv.waitkey(20) & 0xFF == ord('d'):
            break
    capture.release()
    cv.destroyAllWindows()

##### Chờ phím và kiểm tra điều kiện thoát:
    if cv.waitkey(20) & 0xFF == ord('d'):
        break
- `cv.waitKey(20)`: Chờ 20ms trước khi tiếp tục vòng lặp, giúp video chạy đúng tốc độ.
- `& 0xFF == ord('d')`: Kiểm tra nếu người dùng nhấn phím `'d'`, chương trình sẽ thoát khỏi vòng lặp.

##### Giải phóng tài nguyên và đóng cửa sổ:
    capture.release()
    cv.destroyAllWindows()
    
- `capture.release()`: Giải phóng tài nguyên video.
- `cv.destroyAllWindows()`: Đóng tất cả cửa sổ hiển thị.
