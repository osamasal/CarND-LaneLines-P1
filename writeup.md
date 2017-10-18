# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Reflection

For this project, I used the standard pipeline covered in the "finding lane lines on the road" lesson.

To do this, I did the following:

1) Created a grayscale image from the original image and applied Gaussian blur.

2) Applied Canny algorithm to create an image containing all edges, then a ROI mask to mask out any unwanted edges.

3) Used Hough transformation to collect a list of lines for both lanes.

4) Wrote a seperate_lines lines method which separated the left lines from the right lines based on each line slope.
   As part of this, I calculate the avg. slope for each collection of line segments (left lines vs. right lines).

5) I then calculate the avg. line segment for each side and use this information to extrapolate full lines from the 
   bottom of the screen to the top edge (where the image mask starts) and draw the two lane lines on the original image.

Please note that I didn't modify the draw_lines() function directly, instead, I performed all my work in helper functions
which I called from my main function. I then called cv2.line() method to draw the final extrapolated lines.

Here's a sample image were the left and right lines were separated using Hough transformation:
![alt text](https://github.com/osamasal/CarND-LaneLines-P1/blob/master/solidYellowCurve2_Hough.jpg)

The final processed image can be found here:
![alt text](https://github.com/osamasal/CarND-LaneLines-P1/blob/master/solidYellowCurve2.jpg)


### 2. Identify potential shortcomings with your current pipeline

There are several short comings that I can think of when using the method I used:

1) The final extrapolated line is a single line, meaning that it doesn't work very well when the car is going through
   a curve.

2) When playing the two videos, I see that the lines are a bit jittery.

3) To get things working, I changed some of the parameters to make the image less jittery. There is probably a better way to go 
   about figuring out what parameters to use.
   
4) I didn't test this work with different light conditions (e.g. with tree shades), but I suspect that it won't work very well if
   not enough lines are detected due to varying light conditions.

### 3. Suggest possible improvements to your pipeline

1) Generate several connected line segments for each lane instead of a single line for each lane. This should help address 
   the "going" through a curve problem above (#1).

2) Use some smoothing algorithm to get rid of the jittery lines. Perhaps one can average the lines across multiple frames?