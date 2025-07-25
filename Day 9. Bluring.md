# Day 9. Bluring

import cv2 

img = cv2.imread("D:\\image\\sky.jpg")
cv2.imshow("Original Image",img)

#Bluring
blur = cv2.blur(img , (5,5))
cv2.imshow("Blurred Image",blur)

#Gaussian Bluring
gaussian = cv2.GaussianBlur(img,(5,5),0)
cv2.imshow("Gaussian Blurred Image",gaussian)

#Median Bluring
median = cv2.medianBlur(img,5)
cv2.imshow("Median Blured Image",median)

#Bilateral
bilateral = cv2.bilateralFilter(img,10,50,50)
cv2.imshow("Literal Blurred Image",bilateral)

cv2.waitKey(0)
cv2.destroyAllWindows()