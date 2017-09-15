# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[gray]: ./otpt_images/gray.jpg "Grayscale"
[gaus]: ./otpt_images/gaus.jpg "Gaussian Blur"
[canny]: ./otpt_images/canny.jpg "Canny Edges"
[mask]: ./otpt_images/masked.jpg "Masked"
[hough]: ./otpt_images/huffLines.jpg "Hough Lines"
[mask2]: ./otpt_images/mask2.jpg "Masked Again"
[final]: ./otpt_images/final.jpg "Final"
---

### Reflection

### 1. The Pipeline
My pipeline consisted of 7 steps. 

 - Get the grayscale version of the image.

 ![Grayscale][gray]

- Apply Gaussian Blur, with a kernel size of 5

![Gaussian Blur][gaus]

- Apply Canny Edge detection

![Canny Edges][canny]

- Apply region of Interest mask.

![Region of Interest][mask]

- Apply Hough Lines transform.

![Hough Lines][hough]

- Apply region of interest mask again to remove any lines outside this region

![Masked Again][mask2]

- Apply weighted image to the final masked image.

![Final][final]

#### The Draw Lines Function

The Draw lines function was modified to extrapolate lines based on the slope of the detected lines.
 - Towards the base of the image, the lines are extrapolated till the bottom of the image.
 - Towards the top, the lines are extrapolated towards the border of the Region of Interest in increments proportional to the line length.

In cases that the extrapolated line breaches the region of interest, another pass of masking is done to restrict lines to the region of interest.

### 2. Identify potential shortcomings with your current pipeline

- The region of interest is defined statically.
- Lines extrapolated can breach region of interest and another pass of the masking function is needed.


### 3. Suggest possible improvements to your pipeline

 - Dynamically generate region of interest.
   - If the region of interest is defined based on the location of our view, we can better extrapolate lines and curves.
   - Also identifying horizontal edges towards the bottom of the view can provide the base of the region of interest polygon.
 -  Curve identification and extrpolation.
