# Day 2 Resize and Re-scaling

##### Python:
	def rescaleFrame(frame , scale = 0.75):
		width = int(frame.shape[1] * scale)
		height = int(frame.shape[0] * scale)
		dementions = (width , height)
		return cv.resize(frame , demensions  , interpolation=cv.INTER_AREA)
> Hàm rescaleFrame() nhận vào 1 frame(khung hình) và 1 scale(tỉ lệ) , rồi thay đổi kích thước của frame theo tỉ lệ đó , Cuối cùng nó trả về 1 frame đã được resized
##### 1.parameter:
- frame : 1 hình ảnh hoặc một khung hình từ video cần thay đổi kích thước
- scale : đây là tỉ lệ để thay đổi kích thước (mặc định 0.75 , tức là giảm xuống 75% so với kích thước ban đầu)
##### 2.Tính toán kích thước của frame:
- frame.shape[1] : Chiều rộng của hình ảnh
- frame.shape[0] : Chiều cao của hình ảnh
- Lưu ý khi tính toán width và height thì cần ép về interger vì OPENCV yêu cầu kích thước là số nguyên 
-  Lưu kích thước vào 1 tuple
##### 3.Trả về kết quả:
- cv.resize() : hàm của OPENCV để thay đổi kích thước hình ảnh
- dimen : kích thước mới (w,h) sau khi tính toán
- interpolation = cv.INTER_AREA : phương pháp nội suy INTER_AREA thường được dùng để giảm kích thước hình ảnh mà không bị mất chất lượng