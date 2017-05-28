#**Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md 

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)


Creating a Great Writeup
---
For this project, a great writeup should provide a detailed response to the "Reflection" section of the [project rubric](https://review.udacity.com/#!/rubrics/322/view). There are three parts to the reflection:

Reflection

1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.

First, I converted the images to grayscale
then I define a kernel size and apply gaussian smoothing
define parameters for canny and apply to the image
next we'll create a masked edges image using cv2.fillPoly, and set the rest of image to black
Define Hough transform parameters and run the Hough transform on masked edge detection image
Draw the lines segments
Average and extrapolated the line segments to get the full extent of the lane
Combine the line image with the original image
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by

Going through all the line segments I detected to seperate them by there slope, and decide which segment are part of the left line v.s. the right line, and save them seperately to left slope array, and right slope array. If slope is negative then its right line, otherwise it's left line. If the line segment is too short, then it's removed to reduce noise.
After that, removing the outliers of the slope that's not within 1.5 standard deviations of the mean slope, using the filtered array to average the slope and intercept of the left lane and right lane
Calculate the intercetion of the left line and right line, and adjust the intercetion by 10 pixcels depends on left/right of the road
Calculate the other end of the line based on the lane slope and intercept.
Draw the line on the original image with cv2.line
alt text

2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the road is turning and winding,
And it's raining/snowing conditions where there be a lot of noise
If during the night, the color will be different, and edge detection might also not as well
I have to tweeck the mask area and hough parameters to train it for test images/videos, it might not be adaptable to other images, for exmaple where the lane are at different position of the image
If there are cars or obstacles that covers the lane, won't be able to detect and detour

3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...


The Project
---

## If you have already installed the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) you should be good to go!   If not, you should install the starter kit to get started on this project. ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook

You will complete the project code in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an Ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  

**Step 3:** Complete the project and submit both the Ipython notebook and the project writeup

