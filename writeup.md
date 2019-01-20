# **Finding Lane Lines on the Road** 

## Writeup Template

The goals / steps of this project are the following:
    Make a pipeline that finds lane lines on the road.
    Reflect on your work in a written report.


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./output_images/hls_converted_solidYellowCurve2.jpg "ConvertedHLSimage"
[image2]: ./output_images/hls_masked_solidYellowCurve2.jpg "hlsmasked"
[image3]: ./output_images/gray_image_solidYellowCurve2.jpg "Grayimage"
[image4]: ./output_images/gauss_gray_solidYellowCurve2.jpg "Gaussian"
[image5]: ./output_images/Canny_edges_solidYellowCurve2.jpg "Edges"
[image6]: ./output_images/roi_image_solidYellowCurve2.jpg "ROI"
[image7]: ./output_images/Hough_Lines_solidYellowCurve2.jpg "Hough_Lines"
[image8]: ./test_images_output/annotated_solidYellowCurve2.jpg "Line_segment"
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...
In this project, I used Python and OpenCV to find the lane lines and creating averaged and extrapolated boundary line.
**My pipeline consists of following steps,**


1.Convert original image to HSL. 

![alt text][image1]

2.Isolate yellow and white from HLS image

3.Combine isolated HLS with original image

![alt text][image2]

4.Convert image to grayscale.

![alt text][image3]

5.Apply Gaussian Blur to smoothen the gray image for better edges detection.

![alt text][image4]

6.Apply Canny Edge Detection on smoothed gray image to detect edges

![alt text][image5]

7.Trace Region of Interest and discard all other lines identified by canny edge detection that are outside this region 

![alt text][image6]

8. Perform a Hough Transform to find lanes within our region of interest and trace them in red

![alt text][image7]

7.Draw extrapolated lines to extend over detected lane lines.

![alt text][image8]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function and steps followed,
1. separate line segments into left and right lines Using Slope 
2. Then for each line calculate average slopes and intercepts
3. Set height of the image (region of interest image) into the y_max value and find minimum value of y in given lines (set some threshold value of ymin).
4. For both left and right lines:
a)  Calculate x_min and x_max values using intercept, slope, y_min and y_max
b) Draw a line using (x_min, y_min) and (x_max, y_max) for left and Right lanes.



### 2. Identify potential shortcomings with your current pipeline


It only detects the straight lane lines. it fails in fitting curvy lines, the same project can be extending for detecting curve lines.


### 3. Suggest possible improvements to your pipeline

1.One possible improvement could be to avoid shakiness of lines drawn in video .

2.Another possible improvement could be selecting the Better tuning parameters (vertices, threshold)
