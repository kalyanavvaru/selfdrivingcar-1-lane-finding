# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[Lane detections]: ./test_images_output/extrapolated_solidWhiteCurve.jpg


---

### Reflection

Basically started off using code templates in the course videos as starting point. Using these building blocks that does a specific computer vision processing activity, I have stitched together as a pipeline to get the desired objective.


The building blocks of my solution includes 
1. Converting image to gray scale - As we dont need colour to detect edges we try to reduce the noise by clearing the unnecessary colour channel

2. Applied 'Canny edge detection' to find pixels that indicate gradient(change in magnitude) of intensity of pixels. It also does some guassian smoothing behind the scenes to smooth out pixelated edges.

3. Create a region of interest in the image to a polygon area where the lanes may be located in the image to focus only on lanes in the image.

4. Create a hough transform over the image to create lines. This works by mapping image pixes from cartesian space to hough space based on `ro` and `theta`. This transformed space enable calculated on lanes out of pixels via a voting system to indicate pixels that forming a lane. At this point the lines are detected only for paint marking on either lanes.

5. Once the paint lane markings are identified, need to extrapolate such that the detected lane covers the whole representative imaginary lane. This is done by grouping lanes into left lane and right lane based on their slope. THen the points are used to calculate lane coefficients, which inturn were used to draw out the lanes to the whole. 

   ![Lane detections]

6. When a videos is processed for every frame above processing is done and lane annotations are drawn.

### 2. Identify potential shortcomings with your current pipeline


1. Probably would not detect if there are shades that cover the lanes
2. Probably would not work if there is curvature in the visual space


### 3. Suggest possible improvements to your pipeline

1. Need to cater for curves in lanes. May be higher order polynomial need to be used for line fiting.