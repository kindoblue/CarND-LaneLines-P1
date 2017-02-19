#**Finding Lane Lines on the Road** 

##Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

My pipeline consisted of 5 steps. 

 1. I converted the images to grayscale
 2. I blurred the image to filter the high frequencies away, so the canny 
    processing could work better. 
 3. I discarted all the pixel out of a region of interest, defined as an 
    isosceles trapezoid.
 4. I applied the hough transform to detect lines starting from the canny edges.
 5. I drawed the lines on top of the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() 
function by adding code to discriminate the positive and negative slopes. Then 
I accumulated separately all the slopes for right and left and calculated an average. 
I did the same for the intercepts. Once I have the average slope and intercept 
I just intersect this line with the top and bottom of the trapezoid to find the 
top and bottom points needed for cv2.line. 


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when we are on a curve: the
average slope and intercept could not fit perfectly. 

Also spurious lines within the region of interest may affect the average slope. 


###3. Suggest possible improvements to your pipeline

The calculation for the average slope is somewhat crude and lines jumps around 
in the rendered videos. Maybe the slopes and intercept values from the lines 
could be filtered with a range of admissible values so to discard lines that dont
make sense and influence too much the average line. 
