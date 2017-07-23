# **Finding Lane Lines on the Road** 

---

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

## Reflection

### 1. Pipeline and draw_lines() function modification:

The steps of the detect and draw lane lines pipeline on a sinlge image are:

1. Convert the image to greyscale.
2. Smooth the image via gaussian blur.
3. Apply a canny edge detection algorithm.
4. Mask the image so that we only detect on what we expect to be the field of vision for lane detection.
5. Detect lines with Hough transformation and extrapolate and extend lane lines to be drawn. (This is where the interesting stuff happens, see below).
6. Apply the drawn lane line image to the original image.

How the draw_lines() function is implemented:
* Divide into Left and Right Lanes the points detected in a line based on the slope. 
* Extrapolate the coefficients for the line function using cv2.polyfit.
* Apply the coefficients in a fit function with cv2.poly1d.
* draw Right and Left lane lines based on output of the fit function. 


### 2. Identify potential shortcomings with your current pipeline

Some shortcomings are: 

1. I am assuming a very specific field of vision for detecting the lanes, 
where I assume where the horizon will be. This field of vision (i.e. the region of interest)
should be dynamic and change when going up or down a steep hill.
2. As is the case in the optional challenge, the steep turn breaks this pipeline because
it does not account for the varying slope of candidate lines.
3. I am only detecting lines and not curves.

### 3. Suggest possible improvements to your pipeline

One improvement would be to have error detection and multiple algorithms to detect lanes based
on different conditions. As one algorithm detects larger errors (certainty of lane detection is low)
another algorithm with larger certainty takes over. This would create a more dynamic range of solutions.

Another improvement would be to draw curves instead of straight lines. That is to say increase the
dimensionality of the polynomial that describes and draws the lines. 

