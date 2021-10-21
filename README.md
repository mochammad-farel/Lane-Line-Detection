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
