# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

[//]: # (Image References)

[image1]: ./images/grayscale_img.jpg "Grayscale"
[image2]: ./images/blurring_img.jpg  "Blurring"
[image3]: ./images/edges.jpg         "edges"
[image4]: ./images/masked_image.jpg  "masked_image"
[image5]: ./images/line_image.jpg    "line_image"
[image6]: ./images/combo_img.jpg     "combo"
---

### Reflection

### 1. Describe the pipeline. As part of the description, explain how to modify the draw_lines() function.

My pipeline consisted of 6 steps:

1. Convert RGB image to Grayscale image using grayscale() function

![alt text][image1]

2. Smoothing the image to reduce noise using gaussian_blur() function

![alt text][image2]

3. Edge detection using canny() function

![alt text][image3]

4. Define polygon vertices and use region_of_interest() function to create a masked edges image

![alt text][image4]

5. Define Hough transform parameters and use hough_lines() to draw lines. 
In order to draw a single line on the left and right lanes, I modified the draw_lines() function. First I seperate the line segments by slope into 2 list, second I average the coefficient(slope and y-intercept) in each list, third I define y1 and y2, then use the equation    y=mx+b to calculate x1 and x2, finally put those parameters into cv2.line() function.

Explain in Mandarin:
為了在路的左右邊各畫一條線，我修改了draw_lines()，我先算出每條片段的斜率跟截距，接著用斜率把這些片段分出左右邊，再來把左右邊的係數(斜率跟截距)分別取平均值，然後定義y1跟y2後，使用y=mx+b分別求出左右邊的x1與x2，最後將左右邊的x1,y1,x2,y2導入cv2.line()。

![alt text][image5]

6. Overlay two images (input image and line image from Hough transform) using weighted_img function

![alt text][image6]




### 2. Identify potential shortcomings with my current pipeline

1. One potential shortcoming would be it cannot draw curve, when the road is not straight, the program might draw some lines that doesn't fit the lane lines. 

2. Another shortcoming could be when there are some objects in your region of interest, the program might fail to draw the lane lines.


### 3. Suggest possible improvements to the pipeline

1. A possible improvement would be to come up a algorithm that can detect and draw curve lines.

2. Another potential improvement could be to find a way to only detect lane lines and ignore other ojbects.
