# **Finding Lane Lines on the Road** 
<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

--- 
[//]: # (Image References)

[image1]: ./examples/1.jpg "Original"
[image2]: ./examples/2.jpg "Grayscale"
[image3]: ./examples/3.jpg "Canny Edge Detection"
[image4]: ./examples/4.jpg "Region Masking"
[image5]: ./examples/5.jpg "Hough Transform"
[image6]: ./examples/6.jpg "Line Extrapolation"
[image7]: ./examples/7.jpg "Final Image"
[gif-fail]: ./examples/fail.gif "Detection fails"
[gif-good]: ./examples/good.gif "Good detection"
---

## Overview

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

The goal of this project is to build an algorithm with OpenCV library to detect lane markings in images/videos and overlay the extrapolated lane markings over the image. It provides the first step in lane extraction to allow further identification and analysis on lane markings such as curvature calculation and distance estimation.

## Lane Extraction Algorithm

The main lane extraction algorithm consists of few steps:

1. Image is imported and converted to grayscale.
![alt text][image2]

2. Image is then passed through Gaussian Blur and Canny Edge Detection.
![alt text][image3]

3. Region of interest masking is applied to the lower triangle to eliminate irrelevant lines in the image.
![alt text][image4]

4. Then Hough Transform is applied to get each smaller line segments.
![alt text][image5]

5. Line segments are filtered, averaged and extrapolated to cover the entire straight line. Only lines within certain range of slopes with respect to the camera perspective are added to the image to minimize Hough Transform noises. 
![alt text][image6]

6. Extrapolated lines are drawn over original image
![alt text][image7]

7. Applied on videos
![alt text][gif-good]

## Potential shortcomings with this pipeline


Currently the pipeline is very dependent on good lighting and clear markings as the line extraction is obtained from Canny Edge Detection and Hough Transform. Shadows, low contrast, broken or blurry lines can decrease the performance of two algorithms needed in this line extraction algorithm. An example can be seen here.

![alt text][gif-fail]


## Potential improvements to the algorithm

To minimize the impact of lighting and shadows, it's possible to do color transformations such as exhancing contrasts and color space conversions. Enhancing contrasts can make darker pixels and bright line markers more distinct while some other color spaces like HSV allow better filtering on selected colors. 
