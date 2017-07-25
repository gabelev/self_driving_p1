# **Detecting Lanes** 

---

![lane detection](lanes.gif)

This was a fun little project from the Udacity Self-Driving car class to detect car lanes.

---

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
