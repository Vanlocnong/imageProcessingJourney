# Day 8. Color channels

import cv2 
import numpy as np

img = cv2.imread("D:\\image\\sky.jpg")
cv2.imshow("Original Image",img)
blank = np.zeros(img.shape[:2], dtype='uint8')
cv2.imshow("Blank",blank)import cv2 
import numpy as np

img = cv2.imread("D:\\image\\sky.jpg")
cv2.imshow("Original Image",img)
blank = np.zeros(img.shape[:2], dtype='uint8')
cv2.imshow("Blank",blank)
# split the image into its color channels

b,g,r = cv2.split(img)

cv2.imshow("Blue Channel", b)
cv2.imshow("Green Channel", g)
cv2.imshow("Red Channel", r)

# merge the channels back together

merged = cv2.merge([b, g, r]) 
cv2.imshow("Merged Image", merged)   

print("Original Image Shape : " , img.shape)
print("Merged Image Shape:", merged.shape)
print("Blue Channel Shape:", b.shape)
print("Green Channel Shape:", g.shape)
print("Red Channel Shape:", r.shape)
import cv2 
import numpy as np

img = cv2.imread("D:\\image\\sky.jpg")
cv2.imshow("Original Image",img)
blank = np.zeros(img.shape[:2], dtype='uint8')
cv2.imshow("Blank",blank)
# split the image into its color channels

b,g,r = cv2.split(img)

cv2.imshow("Blue Channel", b)
cv2.imshow("Green Channel", g)
cv2.imshow("Red Channel", r)

# merge the channels back together

merged = cv2.merge([b, g, r]) 
cv2.imshow("Merged Image", merged)   

print("Original Image Shape : " , img.shape)
print("Merged Image Shape:", merged.shape)
print("Blue Channel Shape:", b.shape)
print("Green Channel Shape:", g.shape)
print("Red Channel Shape:", r.shape)

blue = cv2.merge([b, blank, blank])
green = cv2.merge([blank,g, blank])
red = cv2.merge([blank, blank,r])
cv2.imshow("Blue", blue)
cv2.imshow("Green", green)
cv2.imshow("Red", red)
cv2.waitKey(0)
cv2.destroyAllWindows()import cv2 
import numpy as np

img = cv2.imread("D:\\image\\sky.jpg")
cv2.imshow("Original Image",img)
blank = np.zeros(img.shape[:2], dtype='uint8')
cv2.imshow("Blank",blank)
# split the image into its color channels

b,g,r = cv2.split(img)

cv2.imshow("Blue Channel", b)
cv2.imshow("Green Channel", g)
cv2.imshow("Red Channel", r)

# merge the channels back together

merged = cv2.merge([b, g, r]) 
cv2.imshow("Merged Image", merged)   

print("Original Image Shape : " , img.shape)
print("Merged Image Shape:", merged.shape)
print("Blue Channel Shape:", b.shape)
print("Green Channel Shape:", g.shape)
print("Red Channel Shape:", r.shape)

blue = cv2.merge([b, blank, blank])
green = cv2.merge([blank,g, blank])
red = cv2.merge([blank, blank,r])
cv2.imshow("Blue", blue)
cv2.imshow("Green", green)
cv2.imshow("Red", red)
cv2.waitKey(0)
cv2.destroyAllWindows()
blue = cv2.merge([b, blank, blank])
green = cv2.merge([blank,g, blank])
red = cv2.merge([blank, blank,r])
cv2.imshow("Blue", blue)
cv2.imshow("Green", green)
cv2.imshow("Red", red)
cv2.waitKey(0)
cv2.destroyAllWindows()
# split the image into its color channels

b,g,r = cv2.split(img)

cv2.imshow("Blue Channel", b)
cv2.imshow("Green Channel", g)
cv2.imshow("Red Channel", r)

# merge the channels back together

merged = cv2.merge([b, g, r]) 
cv2.imshow("Merged Image", merged)   

print("Original Image Shape : " , img.shape)
print("Merged Image Shape:", merged.shape)
print("Blue Channel Shape:", b.shape)
print("Green Channel Shape:", g.shape)
print("Red Channel Shape:", r.shape)

blue = cv2.merge([b, blank, blank])
green = cv2.merge([blank,g, blank])
red = cv2.merge([blank, blank,r])
cv2.imshow("Blue", blue)
cv2.imshow("Green", green)
cv2.imshow("Red", red)
cv2.waitKey(0)
cv2.destroyAllWindows()