# **Project 01: Finding Lane Lines on the Road**

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Overview


### This repo provides a pipeline of deteting lane lines from both image and video for autonomous vehicle(AV) using traditional computer vision techniques, *i.e.* Canny edge detection and hough transform approaches

## Pipeline


### My pipeline consisted of following steps

* Read in image and convert it to grayscale with yellow color enhanced when necessary.
* Define a kernel size and apply Gaussain smoothing `cv2.GaussianBlur()`, which is essential to suppressing noise and spurious gradients by averaging.
* Define low and high thresholds and run Canny edge detection`cv2.Canny()`
![alt text][image1]
* Select region of interest(ROI) `cv2.fillPoly()`
![alt text][image2]
* Define Hough transform parameters, apply Hough transform`cv2.HoughLinesP()` in ROI image to obtain lane line data.
* Group the obtained lane line data into left and right,
* Generate the result by weighted summation of lane line image and the initial image
![alt text][image3]

Note: The above pipeline needs tuning parameters for images from differen sources,*i.e.* image size, boundaries of ROI, parameters for Canny edge detection and Hough transform, etc

## Image Test Results


### Detection with extrapolated line drawn

![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]
![alt text][image8]
![alt text][image9]

## Video Test Results


### Test video 1: `solidWhiteRight.mp4`

![alt text][image10]

### Test video 2: `solidYellowLeft.mp4`

![alt text][image11]

### Test video 3: `challenge.mp4`

![alt text][image12]

## Shortcomings


### There are a few shortcomings in current version of solution

* Only linear lane can be found using this solution with acceptale accuracy. As for curve lane, the linear approximation method might lead to remarkable error(see test video 3 `challenge.mp4`).
* The algorithm is not so robust as it fails to group left or right lane correctly in some of frames in test video 2 `solidYellowLeft.mp4`.
* Bad weather conditions (snow, rain, etc.) and poor light contions will greatly affect the result.
* In this solution, the lane line detection result is based on the selection of ROI. It's acceptable to mask a ROI mannually for input videos comes from similar scenarios. However, complex and changeful scenarios might occur when AVs come into real road. This mannual selection approach undermines the accuracy and generalization of this solution.


## Future Work


### Following aspects can be taken into consideration to boost the solution in the future

* Image from infrared camera can be used
* Add an outlier reduction approach like RANSAC on the hough lines

[//]: # (Image References)
[image1]: ./test_images_output/solidWhiteRight_PreProcess.jpg
[image2]: ./test_images_output/solidWhiteRight_roi.jpg
[image3]: ./test_images_output/solidWhiteRight_lane.jpg
[image4]: ./test_images_output/solidWhiteCurve.jpg
[image5]: ./test_images_output/solidWhiteRight.jpg
[image6]: ./test_images_output/solidYellowCurve.jpg
[image7]: ./test_images_output/solidYellowCurve2.jpg
[image8]: ./test_images_output/solidYellowLeft.jpg
[image9]: ./test_images_output/whiteCarLaneSwitch.jpg
[image10]: ./test_videos_output/solidWhiteRight.gif
[image11]: ./test_videos_output/solidYellowLeft.gif
[image12]: ./test_videos_output/challenge.gif