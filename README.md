### Lane Line Detection Project

## Overiew
These projects are designed to make a detection of lane lines in a road by making perspective transform on images and make detection programs to detect lane lines to implement on dash cam footage.

## Steps
There are steps for making these project:
- camera calibration and distortion correction
- gradient and color thresholding
- perspective transform
- lane line search optimaztion
- make the lane overlay


## Camera Calibration and Distortion Correctnes
Sometimes when we take a picture using cellphone or camera, there's might be a chance of distortion in a picture. Distortion means that deformations of an image appear to be curved than straight. So to face lens distortion, we needs to make an calibration program that could change image from distorted into straight. To be able to do that, we need make a matrix transformation to each unique value in distorted image because distorted image just a linear matrix transformation.

To do that we need to generate an chess image to make calibration by store the object points on the chess images. Because an chess image have 10 columns and 7 rows, we need to focus the object point in the inner side without outer edges, so from 10 columns and 7 rows change into 9 columns and 6 columns without outer edges.
![github image](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/camera_cal/calibration1.jpg)

Object points are made by multiply columns and row image with matrix of 3x3 with data type of 32, we apply this because we want to make a list of (x, y, z) to coordinates for each combination, while x, y values are set and  z values will set to be zero since we working through 2D images, after that, the objects point are mapped using OpenCV module cv2.drawChessboardCorners. It should look like this after applying OpenCV.
[images]

## Gradient and Color Thresholding
for the gradients are using sobel, magnitude and direction gradient, for sobel gradients are used with two axis x and y, this method would likely applied in canny edge detection. This is how it works, the image are converted into grayscale using OpenCV library, after that, setting up the sobel gradient for x and y  axis and calculate the gradients by multiply it to 255(because image have an RGB color) and divide it with the maximum of the gradient.

applying the magnitude gradient into image, the process are likely same as we apply the sobel gradient in canny edge, the difference is in the gradient calculation, the purpose of applying gradients magnitude is to measure how strong the change in image intensity. and the last one direction gradient is used to filter the direction of gradient.

For color thresholding, choose Hue Saturation Lightness or HSL color space to retain information about the lane lines in a picture and Red channel filters is used for creating binary lane line images.

All of that are combined together in a pipeline, which resulting this

![github image](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/saved_figures/combined_filters.png)

## Perspective Transform
Perspective transform are created to remove extra information in the images and focusing on the lines in the image. To do that, we have to generate linear matrix transform by using Opencv module which is getsPerpectiveTransform and warpPerspective. apply it on an image which resulting this polygon line on the images.
![github image](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/saved_figures/perspective_transform.png)

After the linear matrix are formed, now we had to look at histogram distribution to checking the quality of the transformed image
![github_image](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/saved_figures/lane_histogram.png)

## Lane Line Search Optimization
For lane line search optimization, we could create:
- search window on the bottom of the image
- split the window into two halves which is left halves and right halves
- locate the pixel column with the highest value
- make a drawable box in the area using margin variable
- identifying value for non-zero pixels in the drawable box
- fitting quadratic equation to all non-zero pixels value
After create those six steps. resulting  this
![github image](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/saved_figures/01_window_search.png)

## Make Lane Overlay
Now in this section, we could generate quadratic equation to generate polynomial output. After that we could use cv2.fillpoly to filling the polynomial output and cv2.warpPerspective to unwarp the images. The result is this.
![github image](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/saved_figures/lane_polygon.png)

## Result
After overlay are created, now we implement it on the dashcam footage
![caption](https://github.com/mochammad-farel/Lane-Line-Detection/blob/main/videos/chicago_lanelines.mp4 / GIF)
