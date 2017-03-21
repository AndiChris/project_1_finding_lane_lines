**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consist of 5 steps. First I convert the image to grayscale, then I apply a gaussian blur filter with a kernelsize of 5 to smoothen hard gradients and prepare the image best for the next step the Canny-edge detection.

After the Canny edge-detection was applied I apply a mask on the output so that just a certain region (namely the one were we expect the lanes to be) is left.

The next step is a Hough-Transformation after which the openCV HoughLinesP function can extract lines easily when called with good parameters.

In order to draw a single line on the left and right side of the lane, I modified the draw_lines() function by calculating the slope of every line and deciding if it seems to be either a left line with a negative slope or a right line with a positive slope. I store everything in two distinct numpy arrays and run the numpy average function on the data. Additionally I add as a weight (for the average function) the length of each line.

Afterwards I calculate the remaining parameter b from the line equation y=mx+b (b=y-mx). With this final line equation and fixed y values (boundary of my range_of_interest shape and the image dimensions) I determine the final x1,y1 and x2,y2 values and draw one big line for each side into the image.


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be that vertical lines are skipped since they have infinite slope and would need separate treatment.


###3. Suggest possible improvements to your pipeline

One possible improvement could be to store some history of the average values throughout multiple images which then run into the average calculation of the next image. Maybe this way the lines would be more stable when run on a video. Additionally one could sort out outliers which seem to be way of the other lines.

Maybe another improvement could be to use the numpy library polyfit function with higher degree polynomials (not just like the simple line equation above) to get some nicer curves.

