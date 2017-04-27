##Writeup Template
###You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

Undistorted Chessboard images
[image1]: ./output_images/calibration_undist1.jpg "Undistorted-1"
[image2]: ./output_images/calibration_undist1.jpg "Undistorted-2"
[image3]: ./output_images/calibration_undist1.jpg "Undistorted-3"
[image4]: ./output_images/calibration_undist1.jpg "Undistorted-4"
[image5]: ./output_images/calibration_undist1.jpg "Undistorted-5"
[image6]: ./output_images/calibration_undist1.jpg "Undistorted-6"
[image7]: ./output_images/calibration_undist1.jpg "Undistorted-7"
[image8]: ./output_images/calibration_undist1.jpg "Undistorted-8"
[image9]: ./output_images/calibration_undist1.jpg "Undistorted-9"
[image10]: ./output_images/calibration_undist1.jpg "Undistorted-10"
[image11]: ./output_images/calibration_undist1.jpg "Undistorted-11"
[image12]: ./output_images/calibration_undist1.jpg "Undistorted-12"
[image13]: ./output_images/calibration_undist1.jpg "Undistorted-13"
[image14]: ./output_images/calibration_undist1.jpg "Undistorted-14"
[image15]: ./output_images/calibration_undist1.jpg "Undistorted-15"
[image16]: ./output_images/calibration_undist1.jpg "Undistorted-16"
[image17]: ./output_images/calibration_undist1.jpg "Undistorted-17"
[image18]: ./output_images/calibration_undist1.jpg "Undistorted-18"
[image19]: ./output_images/calibration_undist1.jpg "Undistorted-19"
[image20]: ./output_images/calibration_undist1.jpg "Undistorted-20"

Undistorted road test images
[image21]: ./output_images/undist0.jpg "Undistorted-Testimage-1"
[image22]: ./output_images/undist1.jpg "Undistorted-Testimage-2"
[image23]: ./output_images/undist2.jpg "Undistorted-Testimage-3"
[image24]: ./output_images/undist3.jpg "Undistorted-Testimage-4"
[image25]: ./output_images/undist4.jpg "Undistorted-Testimage-5"
[image24]: ./output_images/undist5.jpg "Undistorted-Testimage-6"
[image25]: ./output_images/undist6.jpg "Undistorted-Testimage-7"

Thresholded images (source undistorted test images)
[image26]: ./output_images/Pipeline0.jpg "Thresholded image-1"
[image27]: ./output_images/Pipeline1.jpg "Thresholded image-2"
[image28]: ./output_images/Pipeline2.jpg "Thresholded image-3"
[image29]: ./output_images/Pipeline3.jpg "Thresholded image-4"
[image30]: ./output_images/Pipeline4.jpg "Thresholded image-5"
[image31]: ./output_images/Pipeline5.jpg "Thresholded image-6"
[image32]: ./output_images/Pipeline6.jpg "Thresholded image-7"

Perspective transformed image (source Thresholded test)
[image33]: ./output_images/top_down0.jpg "Perspective transformed image-1"
[image34]: ./output_images/top_down1.jpg "Perspective transformed image-2"
[image35]: ./output_images/top_down2.jpg "Perspective transformed image-3"
[image36]: ./output_images/top_down3.jpg "Perspective transformed image-4"
[image37]: ./output_images/top_down4.jpg "Perspective transformed image-5"
[image38]: ./output_images/top_down5.jpg "Perspective transformed image-6"
[image39]: ./output_images/top_down6.jpg "Perspective transformed image-7"

Final Images
[image40]: ./output_images/final0.jpg "Final image-1"
[image41]: ./output_images/final1.jpg "Final image-2"
[image42]: ./output_images/final2.jpg "Final image-3"
[image43]: ./output_images/final3.jpg "Final image-4"
[image44]: ./output_images/final4.jpg "Final image-5"
[image45]: ./output_images/final5.jpg "Final image-6"
[image46]: ./output_images/final6.jpg "Final image-7"

Centroid Windows Images
[image47]: ./output_images/win_centroid0.jpg "Sliding-Win image-1"
[image48]: ./output_images/win_centroid1.jpg "Sliding-Win image-2"
[image49]: ./output_images/win_centroid2.jpg "Sliding-Win image-3"
[image50]: ./output_images/win_centroid3.jpg "Sliding-Win image-4"
[image51]: ./output_images/win_centroid4.jpg "Sliding-Win image-5"
[image52]: ./output_images/win_centroid5.jpg "Sliding-Win image-6"
[image53]: ./output_images/win_centroid6.jpg "Sliding-Win image-7"

[video1]: ./project_marked_lanes.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points
###Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!
###Camera Calibration

####1. Around twenty images of chessboards were provided with the project to calibrate the cameras.
The camera calibration process is a two step process.
The first exercise was to calibrate the camera by first getting the corners using OpenCV findChessboardCorners. We use drawChessBoardCorners to verify the points).
Using the image and object points so obtained, we can calibrate the camera.
arround 17 of the above images were used to perform camera calibration.

The code for this step is contained in the fourth and fifth code cell's of the Jupyter notebook located in "./Advnced_lanes.ipynb".

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the chessbord and test images using the `cv2.undistort()` function and obtained this result: 


####1. Provide an example of a distortion-corrected image.
To demonstrate this step, I will describe how I apply the distortion correction to all of the Calibration and test images:

Undistorted Chessboard images
[image1]: ./output_images/calibration_undist1.jpg "Undistorted-1"
[image2]: ./output_images/calibration_undist1.jpg "Undistorted-2"
[image3]: ./output_images/calibration_undist1.jpg "Undistorted-3"
[image4]: ./output_images/calibration_undist1.jpg "Undistorted-4"
[image5]: ./output_images/calibration_undist1.jpg "Undistorted-5"
[image6]: ./output_images/calibration_undist1.jpg "Undistorted-6"
[image7]: ./output_images/calibration_undist1.jpg "Undistorted-7"
[image8]: ./output_images/calibration_undist1.jpg "Undistorted-8"
[image9]: ./output_images/calibration_undist1.jpg "Undistorted-9"
[image10]: ./output_images/calibration_undist1.jpg "Undistorted-10"
[image11]: ./output_images/calibration_undist1.jpg "Undistorted-11"
[image12]: ./output_images/calibration_undist1.jpg "Undistorted-12"
[image13]: ./output_images/calibration_undist1.jpg "Undistorted-13"
[image14]: ./output_images/calibration_undist1.jpg "Undistorted-14"
[image15]: ./output_images/calibration_undist1.jpg "Undistorted-15"
[image16]: ./output_images/calibration_undist1.jpg "Undistorted-16"
[image17]: ./output_images/calibration_undist1.jpg "Undistorted-17"
[image18]: ./output_images/calibration_undist1.jpg "Undistorted-18"
[image19]: ./output_images/calibration_undist1.jpg "Undistorted-19"
[image20]: ./output_images/calibration_undist1.jpg "Undistorted-20"

Undistorted road test images
[image21]: ./output_images/undist0.jpg "Undistorted-Testimage-1"
[image22]: ./output_images/undist1.jpg "Undistorted-Testimage-2"
[image23]: ./output_images/undist2.jpg "Undistorted-Testimage-3"
[image24]: ./output_images/undist3.jpg "Undistorted-Testimage-4"
[image25]: ./output_images/undist4.jpg "Undistorted-Testimage-5"
[image24]: ./output_images/undist5.jpg "Undistorted-Testimage-6"
[image25]: ./output_images/undist6.jpg "Undistorted-Testimage-7"

###Pipeline (single images)

####2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.
I used a combination of color and gradient thresholds to generate a binary image. This is in cell 9 of the Jupyter Noteboook.  Here's an example of my output for this step.  

Thresholded images (source undistorted test images)
[image26]: ./output_images/Pipeline0.jpg "Thresholded image-1"
[image27]: ./output_images/Pipeline1.jpg "Thresholded image-2"
[image28]: ./output_images/Pipeline2.jpg "Thresholded image-3"
[image29]: ./output_images/Pipeline3.jpg "Thresholded image-4"
[image30]: ./output_images/Pipeline4.jpg "Thresholded image-5"
[image31]: ./output_images/Pipeline5.jpg "Thresholded image-6"
[image32]: ./output_images/Pipeline6.jpg "Thresholded image-7"

####3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

The code for my perspective transform includes a function called `corners_unwarp()`, which appears in cell 11 of the Jupyter notebook.  The `corners_unwarp()` function takes as inputs an image (`img`),  and returns the warped, M and MINV values.
I chose the hardcode the source and destination points in the following manner:

    src = np.float32([[524,500], [203,700],[1125,700],[759,500]])
    dst = np.float32([[300,0], [300, 720], [1088,720], [1088,0]])

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

Perspective transformed image (source Thresholded test)
[image33]: ./output_images/top_down0.jpg "Perspective transformed image-1"
[image34]: ./output_images/top_down1.jpg "Perspective transformed image-2"
[image35]: ./output_images/top_down2.jpg "Perspective transformed image-3"
[image36]: ./output_images/top_down3.jpg "Perspective transformed image-4"
[image37]: ./output_images/top_down4.jpg "Perspective transformed image-5"
[image38]: ./output_images/top_down5.jpg "Perspective transformed image-6"
[image39]: ./output_images/top_down6.jpg "Perspective transformed image-7"

####4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Then I did some other stuff and fit my lane lines with a 2nd order polynomial kinda like this:
First we found the window centroids and identified the starting points in l_center and r_center. Thereafter, I also used the histogram to check if the identified r_center and l_center points are in the expected band.
The histogram also goes through a sanity check to ensure that the histogram provides a valid starting point.
The sliding window then masures the next points for identifying the lane lines.
Since I am using the same function to identify the lane lines for the video, the change in identified points is kept to within 3 pixels. With three pixels per frame, and 48 fps expected video, we can have 132 pixel change which is sufficient variation in actual conditions.
A polyfit functions greates the poly line and fillpoly provides a green layer on the road identifying the lane.
Final the polyfit is un-warped and imposed on the undistorted original image.
I created two lines of class Line(). these lines store the previous and current values of the centroids, left and right fit points, radius of curvature and offset.
if the lane lines are identified (at least 5 centroids on either right or left side have identified points) and centroids gap is fairly in line with expectations, the centroidd is considered good.
based on this, we choose if we use the current measurements or the previous measurement.
For car ffset, we take the difference divided by 20 (to avoid big changes).

####4.1 Sanity Checks:
#####4.1.1 : function do_once: Base detection by two methods. 
We detect the starting point of the lanes using both the sliding windows and the base is fixed at expected points. For project purposes, this is kept at a certain range (380-450 pixels on left  and 875-975 on right)
#####4.1.2 find_window_centroids :
Left and right center validity is checked (at least 40 pixels are detected in that centroid. if not then we take offset from either right or left that is detected. This will ensure that the lane widths are not too off.
#####4.1.3 find_window_centroids :
Left and right widths validity is checked (between 475 and 525 in this case). Thos goes to a calculation that will use previous centroid values if widths are not proper or 4.1.2 fails
#####4.1.4 find_window_centroids :
by using the track class, we are averaging the centroids over a defined smoothfactor. This will disallow too fast variations in video frames.
#####4.1.5 function centroids:
the base fitx points used for all calculations for lane side colors, lane coloring, curve radius is checked for too much variation by cv2.matchShapes function. Old values are used if variation is too high.
#####4.1.6 function centroids:
bad curve value detection: if the left and right curve radius change by more than 100 meters, or if the values are too low, old values are used.


Centroid Windows Images
[image47]: ./output_images/win_centroid0.jpg "Sliding-Win image-1"
[image48]: ./output_images/win_centroid1.jpg "Sliding-Win image-2"
[image49]: ./output_images/win_centroid2.jpg "Sliding-Win image-3"
[image50]: ./output_images/win_centroid3.jpg "Sliding-Win image-4"
[image51]: ./output_images/win_centroid4.jpg "Sliding-Win image-5"
[image52]: ./output_images/win_centroid5.jpg "Sliding-Win image-6"
[image53]: ./output_images/win_centroid6.jpg "Sliding-Win image-7"

####5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in lines #127 through #137 in my code in cell 32 (window_centroids() function)
I also calculated the car offset (how far away from center of lane). This is done by subtracting the center of the lane and the center of the image.
Further the radius of curvature for videos goes through a sanity check using cv2.matchShapes function. So if wither of the right or left points of the fitx (right_fitx or left_fitx) are not currect, we use the older values.


####6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in lines #141 through #151 in my code in windows_centroids() function in cell 32 

Final images are below.
Final Images
[image40]: ./output_images/final0.jpg "Final image-1"
[image41]: ./output_images/final1.jpg "Final image-2"
[image42]: ./output_images/final2.jpg "Final image-3"
[image43]: ./output_images/final3.jpg "Final image-4"
[image44]: ./output_images/final4.jpg "Final image-5"
[image45]: ./output_images/final5.jpg "Final image-6"
[image46]: ./output_images/final6.jpg "Final image-7"
---

###Pipeline (video)

####1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_marked_lanes.mp4)

---

###Discussion

####1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?
Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.

1. Initial isssues: 
I initially used the histogram method for lane identification, but I had some failures, when right_lane_inds produced a null output. I switched to the sliding windows method, but lines were too wobbly.
I then used a combined method.
I also had issues with finding the src and dst points and then after some trial and error, I got the points that helped me in the quest of project completion.
2. Improvements:
I could keep the src and dst outside and pass on the points. These points could have some other calcculations. 
For e.g. 111X7 is used for this example, but when roads become smaller width, say 3 meters, we need to use a different ratio (as in the harder_challenge).
The height of the src would also change when going through harder bends as in harder_challenge video (lower speed = lower area of interest and higher speed = bigger area of interest).
3. Improvements:
have a tabular radii of road curvature and measure major curvatures against the same. However, curvature could be non standard at times.

  

