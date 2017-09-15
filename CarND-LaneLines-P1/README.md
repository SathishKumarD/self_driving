#**Finding Lane Lines on the Road**


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report



---

### Reflection

### Pipeline

**Extract yellow color**
Extracting yellow colors helps identifying the yellow lane. Bitwise mask is used to extract the yellow color.

**Converting the image to grey scale**
An image is represented as a three dimensional matrix. We could extract yellow color and white color for 

**Adding gaussian smoothing**
Taking gradients is very sensitive to noise. So adding gaussian smoothing helps in case of edge detection.


**Canny Edge detection**
In canny edge detection, gradient is taken to find edges. A minimum threshold is applied to reduce noise. Also, strong edges are extended to weak edges to "fill" the gap. But only weak edges are removed. The principle behind the canny edge detection is, an edge will have atleast some strong edges.
We now have edges to find lanes.

**Hugh Transform to find lines**
We restrict the region of interest to find lane lines to avoid noise. We transform cartesian image space to hugh space with co-ordinares ρ and θ where lines in image space is mapped to a point where many sinusoids intersect. 

**Filtering the lines based on slope and Y intercept**
If slope is positive, the lane is left lane. if slope is negative, the lane is right lane. Also, if we restrict the absolute value of slope to less than 0.4 to reduce noise.

**Linear regression to convert all the lines to a single lane line**
Multiple lane lines can be converted into single lane line by running a linear regession on it.

**Moving average smoothing**
Sudden moving lane lines can be fixed by applying moving average.


