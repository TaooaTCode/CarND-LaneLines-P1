
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
1. I converted the images to grayscale;
2. I used Canny edge detector to extract edges in the image. I set the low_threshold=30, high_threshold=450 to have the best result from the test images;
3. I created a mask using cv2.fillPoly to mask out the region of interest in the edge image;
4. I used the function - "hough_lines", to find the strait lines in the edge image. In order to find constant line aligning well with the lane mark, I set the min_line_length = 20, and max_line_gap = 1;
5. The result from "hough_lines" is passed to draw_lines() function to draw the lines on top of the images; 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by aggregating data in two groups - left lanes and right lanes. In order to aggregate the right data and reject outliner, I set bracketed slope thresholds for left lanes and right lanes respectively. The single line's two end points in calculated after aggregating the all the data in one frame and taking their averages. 


If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane is very curved during the car is turning. That will cause a big deviation from the current straight line model. 

Another shortcoming could be if a car or something else in getting into the region of interest, this would potentially create false positive lines pass the bracketed slope thresholds, and degrade the accuracy of single line calculation. 



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to build a lane line model that can curve up to the left and right with limited fitting parameters;

Another potential improvement could be to add object detection that can tell and object is getting into the region of interest, and segmenting out those region. 
