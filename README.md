**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consist of 5 steps. First, I convert the images to grayscale, then I apply a gaussian blur filter with a kernelsize of 5.
After that a Canny edge-detection algorithm is applied and the output is masked so that just a region were I expect the lanes to appear is left.

With a Hough-Transform lines can be extracted easily.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the slope of every line and deciding if it is either a left line with a negative slope or a right line with a positive slope. I stored everything in two distinct numpy arrays and run the numpy average function on the data.

Afterwards I calculated the remaining parameter b from the line equation y=mx+b (b=y-mx). With this final line equation and the fixed y values, namely the boundary of my range_of_interest shape and the image, I determined the final x1,y1 and x2,y2 values and could draw one line for each side into the image.


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be that vertical lines are skipped since they have infinite slope and would need separate treatment.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to smoothen out any outliers in the data so the lines become more stable in position and slope.
