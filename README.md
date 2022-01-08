
![](https://github.com/Leon-Is-Bad-At-Coding/RANSAC/blob/main/output_video.gif?raw=true)



This project uses the RANSAC algorithm to fit a circle model onto the pupil of an eye. The circle model allows us to observe the radius of the pupil and detect blinks. RANSAC stands for Random Sample Consensus. The idea of RANSAC is to fit a model based on only the inliers of a data set. Inliers are points that we want to fit because they are close to other inliers, outliers are points that we don’t want to fit because they are significantly different from the inliers. The parameters for RANSAC are the error threshold (maximum amount of error allowed for a point to be considered an inlier), inlier percentage (minimum percentage of points within the data set that are considered inliers), and number of iterations (number of times the algorithm loops.) You can determine the parameters by visualizing the rough number of inliers, and how tightly they are packed together.

The steps for RANSAC are:
1. Set values for thresholds
2. Choose random points to initialize model
3. Check if the model contains the minimum percentage of inliers, if yes, save model
4. Repeat steps 2-3 until the maximum number of iterations is hit, return best model and error

Robustness is the attribute of being insensitive to noise and outliers. RANSAC is robust because it is not significantly affected by outliers; it only consideres inliers.

![download](https://user-images.githubusercontent.com/84482670/148626880-5fbfaf8a-d2df-4be6-ba69-ee8050db0894.png)

You can use RANSAC on any models that can be estimated with a random sampling of points within the data set and have a measurable error. The circle model object has 3 parameters: x (x coordinate of center), y (y coordinate of center), and radius. It has a circle method which creates a circle object based on 3 points, an error method which computes the error of a point, and an estimate which estimates a circle model based on the object’s parameters. Before fitting circles to each frame, first you convert the frame to greyscale. Then you make it binary so it only contains 2 colours. Then you use the edge detection function on it to draw the edge of the pupil. We want to binarize each frame so our edge detection function outputs a very clean line on the pupil. You want to choose a threshold where only the pupil will be visible. 

A frame contains a blink if there is a large variation in the pupil radius. To filter out blinks, you can plot a graph of pupil radius as a function of frame number and remove frames in which there is a spike.

![download](https://user-images.githubusercontent.com/84482670/148630161-b1c010af-d813-4098-b5fd-18eb86f4acd9.png)
