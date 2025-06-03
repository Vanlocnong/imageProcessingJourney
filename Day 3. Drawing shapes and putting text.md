# Day 3. Drawing shapes and putting text

##### 1. Vẽ full pixel với 1 màu chỉ định:
    import numpy an np
    black_img = np.zeros((500 , 500 ,3) , dtype = "uint8")
    black[:] = 0,255,0 # tất các pixel màu xanh lá
    blank[200:300 , 300,400] = 255,0,0 # Chọn một vùng của ảnh từ pixel hàng 200 đến 300 và cột 300 đến 400.


##### 2.Draw a rectangle:
    cv.rectangle(black_img , (100,100) , (black_img.shape[1] // 2 , black_img.shape[0] // 2) , (255,0,0) , thickness = -1)
    cv.imshow("rectangle" , black_img)

##### 3.Draw a circle:
    cv.circle(black_img , (black_img.shape[1] // 2 , black_img.shape[0] // 2) , 50 , (0,255,0) , thickness= -1)

##### 4.Draw a line
    cv.line(black_img , (0,0) , (black_img.shape[1] -10, black_img.shape[0]-10) , (0,0,255) , thickness=2)

##### 5.Put text:
    cv.putText(black_img , "Hello OpenCV" , (black_img.shape[1] // 2 , black_img.shape[0] // 2) ,cv.FONT_HERSHEY_PLAIN,1,(255,0,0) ,2)