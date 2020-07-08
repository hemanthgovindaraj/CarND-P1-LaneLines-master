# **Finding Lane Lines on the Road** 

## Writeup 

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
First, I converted the images to grayscale, then I performed a smoothening of the image using the gaussian smoothening method.
Next i used the Canny algorithm to detect the thick edges that represent the lines. 
Then, i created a 2 sided polygon to black out  the areas which are unnecessary. On the canny ouput image, the polygon is used to mask the region.
At last i used the Hough transform on the edge detected image to arrive at a processed image which has only the detected lane lines or part of the lane lines. 
Next i apply the lane lines image over the original image to have a final lane detected image.

In order to draw a single line on the left and right lanes, I modified the draw_lines().
First i seperated out the lines as ones with positive slope and ones with the negative slope. 
Then i calculated the average of all the coordinates x1, x2, y1, and y2 of every line to arrive at a single line each with a positive slope and a negative slope.Then i used the coordinates of the averaged out line to calculate the slope and gradient of these lines.
Using these slope and gradient of the line , then using the usual top of the lane and end of the lane y coordinates as the input, i calculate the x coordinates as well. Now using these x and y coordinates, i finally created a single line for the lane lines on the left and right.

Below is a sample of the image after the processing.

![image after processing][./test_images_output/output_solidWhiteCurve.jpg]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen in case the image from the camera is not clear enough to have a good processing for the image. Example - rainy conditions, night time etc

Another shortcoming could be that the vehicle speed is high and the processing time is not fast enough to detect the lane lines.
I have also operated on the assumption that the camera is fixed and the image is always having a similar start and end points.
In certain cases drawing lane line might not make sense, for example in a tight curve.
These are the potential shortcomings that i see.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to sometimes sense that we are in a curve and draw a curve as path and not a lane line.

Another potential improvement could be to improve the processing time to cope with the higher speeds of the vehicle.
