# **Finding Lane Lines on the Road** 


The goal of this project is to locate the land lines in a driving video record.
The images from the video are processed through a pipeline to extract the lane line feature.



## Pipeline design
For every frame in the video, it goes through the following pipeline and extract the lane line feature.
1. Change frame color to grayscale
![](https://i.imgur.com/y1mvSWA.png)
2. Remove spot noise by applying Gaussian smoothing
![](https://i.imgur.com/KdlbFXC.png)
3. Extract edge features by applying Canny transformation
![](https://i.imgur.com/UozdR8U.png)
4. Label the region of interest and mask area outside of it
![](https://i.imgur.com/AnN7TG2.png)
5. Get line segments by applying Hough transform
6. Extract lane lines from line segments
    1. Seperate line segments with slope
    2. Average seperated line segments to define left and right lane
    3. collect prevous line information for missing left and/or right lane images.(This is valid according to [Bayes law](https://en.wikipedia.org/wiki/Bayes%27_theorem))

![](https://i.imgur.com/Wl1tj3p.png)

7. Merge the line into the original image
![](https://i.imgur.com/giWK2b6.png)



## Shortcomings 
### Hard-coded tuning
Some part of the pipeline is tuned and hard-coded according to the given video clips. There can be a high risk that some other video clip might not be suitable for this approach.

### Straight-line assumption
The pipeline assumed that both left and right lane are straight line. So the model will fail when the car is turning. I believe by cutting down the distance my model is trying to predict and spped up the frame frequency, it will still work and the gating  problem becomes efficiency issue.


## Possible improvements
### Tuning can be optimized
During tuning, the parameters are manually tested against visual comparison, i.e. the result is the fairly good one but I have no clue if it can still improve. A test score should be invented in order to quantify the tuning result and find the optimal parameters.
### Video formatter
Although the hard-coded tuning process is aimed at only the given short clip, I believe with the right transformer software, this pipeline can be more generally used on many other video clips. 