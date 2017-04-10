#**Finding Lane Lines on the Road**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consisted of 5 steps.
1. Convert the images to grayscale because we don't need the color information, we just find the line in image

2. Because Canny will do derivate, it is sensitive of high frequency term and these terms may be a noise, We may Blur the image to
eliminate these noise

3. We can ues Canny function to detect all edges in the image, this function will retuen a binary image(edge image), if pixel is detected to be a part of edge, it's value is 255 else is 0

4. Afte we get the edge image we need to detect the line of lane line, before that we know the reasonable area of lane line, so we prepare a mask to restrict the area of line detection and apply it to our edge image then we can use opencv's ***HoughLinesP***
function to get line in the masked area of edge image

5. In order to draw a single line on the left and right lanes, i modified the draw_lines() function by average detected lines's position
    and skip the line has slop less than 0.5(horizontal line ) and large than 0.8(vertical line)


![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is no lane line in the image

Another shortcoming could be wrong line to be detected as a lane line, although i skip lines which has slop is out of 0.5 ~ 0.8
but i am not sure is this a right way ?


###3. Suggest possible improvements to your pipeline

A possible improvement would be dynamic area of lane line detection area
now we just fix the area of detection lane line maybe more situation should be considered

Another potential improvement could be sometimes there is no right/lef lane line is detected
i think we can keep the last detected lane line for the option if there is no lane line detected
