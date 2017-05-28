# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
- First, I converted the images to grayscale
- then I define a kernel size and apply gaussian smoothing
- define parameters for canny and apply to the image
- next we'll create a masked edges image using cv2.fillPoly, and set the rest of image to black
- Define Hough transform parameters and run the Hough transform on masked edge detection image
- Draw the lines segments
- Average and extrapolated the line segments to get the full extent of the lane
- Combine the line image with the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by
- Going through all the line segments I detected to seperate them by there slope, and decide which segment are part of the left line v.s. the right line, and save them seperately to left slope array, and right slope array. If slope is negative then its right line, otherwise it's left line. If the line segment is too short, then it's removed to reduce noise. 
- After that, removing the outliers of the slope that's not within 1.5 standard deviations of the mean slope, using the filtered array to average the slope and intercept of the left lane and right lane
- Calculate the intercetion of the left line and right line, and adjust the intercetion by 10 pixcels depends on left/right of the road
- Calculate the other end of the line based on the lane slope and intercept.
- Draw the line on the original image with cv2.line

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


- One potential shortcoming would be what would happen when the road is turning and winding,
- And it's raining/snowing conditions where there be a lot of noise
- If during the night, the color will be different, and edge detection might also not as well
- I have to tweeck the mask area and hough parameters to train it for test images/videos, it might not be adaptable to other images, for exmaple where the lane are at different position of the image
- If there are cars or obstacles that covers the lane, won't be able to detect and detour


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
