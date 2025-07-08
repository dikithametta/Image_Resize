# Image_Resize

README - Image Resizing using OpenCV and Custom C++


Assignment: Image Resizing using OpenCV and Custom Implementation in C++

This task performs image resizing on a BMP image using both OpenCV's built-in 'cv::resize' function and a custom implementation. It supports three interpolation methods:
1. Nearest Neighbor ('INTER_NEAREST')
2. Bilinear ('INTER_LINEAR')
3. Bicubic ('INTER_CUBIC')

The task benchmarks the time taken to perform 1000 iterations of each method and compares results between OpenCV and the custom implementation.


1. ENVIRONMENT SETUP (Google Colab)
-----------------------------------
I choosed Google Colab to execute this task because it doesn't need any installations while with other platforms you need to install c++ complier and OpenCV separately.
 
1. Open Google Colab in chrome
2. On the Colab home screen:
Click File in that got to Open notebook
Go to the Upload tab
Click “Choose File”, select the .ipynb file from your computer
Click Open

#Install OpenCV and essential build tools:

!apt update
!apt install -y libopencv-dev build-essential

#Monunt Your Google Drive to access image files:
-When you're mounting it will ask for google drive then choose your account and select all and continue.

from google.colab import drive
drive.mount('/content/drive')


2. INPUT
--------
#The input image should be placed in Google Drive if not you will face the error that could not load image

#You can download and upload the input file from the following link:

Input image:
https://avproglobal.egnyte.com/fl/V6JZASnouL

Download G178_2-1080.BMP from above link.


Path: /content/drive/MyDrive/G178_2 -1080.BMP

#It reads using:

cv::Mat src = cv::imread(input_path);

#Ensure the file exists:

import os
print(os.path.exists("/content/drive/MyDrive/G178_2 -1080.BMP"))


3. OUTPUT
---------
#Resized images are saved to:

/content/drive/MyDrive/output_nearest.bmp
/content/drive/MyDrive/output_linear.bmp
/content/drive/MyDrive/output_cubic.bmp

#These files are created using:

cv::imwrite("path", resized_image);


4. FILE 1: resize_image.cpp
---------------------------
Purpose: Resize the input image using 3 different OpenCV interpolation methods and save them.

Key steps:
- Load the image

Resize using:
- INTER_NEAREST
- INTER_LINEAR
- INTER_CUBIC

Save the resized images to Drive.

#How to run:

!g++ resize_image.cpp -o resize_image `pkg-config --cflags --libs opencv4`
!./resize_image


5. FILE 2: resize_image_1000.cpp
--------------------------------
Purpose: Benchmark the performance of OpenCV's interpolation methods for 1000 iterations.

Key Steps:
- Load the image.
- For each interpolation method:
    Perform cv::resize 1000 times.
    Measure the elapsed time using std::chrono.
- Print the execution time for each method.

#Output:

Printed to terminal:
Time taken for 1000 iterations using INTER_NEAREST: 'xxx' ms
Time taken for 1000 iterations using INTER_LINEAR: 'xxx' ms
Time taken for 1000 iterations using INTER_CUBIC: 'xxx' ms

#How to run:

!g++ resize_image_1000.cpp -o resize_image_1000 `pkg-config --cflags --libs opencv4`
!./resize_image_1000


6. FILE 3: resize_image_custom2.cpp
-----------------------------------
Purpose: Implement a custom image resizing function with support for Nearest and Linear interpolation (Cubic is treated as linear),and compare it with OpenCV's results.

Features:
- Implements myResize() function for resizing using pixel sampling.
- Compares OpenCV and custom output with a tolerance of ±2 pixel value difference.
- Benchmarks time for 1000 iterations of both OpenCV and custom implementation.
- Reports similarity (boolean) and timing.

#Comparsion Logic:
bool compareImagesWithTolerance(cv::Mat img1, img2, int tol = 2);

Compares each pixel of both images. If any channel in a pixel exceeds the tolerance, the images are not considered similar.

#Console Output:

Interpolation method: 0 (0=Nearest,1=Linear,2=Cubic)
OpenCV resize time (1000 iters): xxxx ms
Custom resize time (1000 iters): yyyy ms
Outputs similar (tolerance=2)? YES

#How to run:

!g++ resize_image_custom2.cpp -o resize_image_custom2 `pkg-config --cflags --libs opencv4`
!./resize_image_custom2
