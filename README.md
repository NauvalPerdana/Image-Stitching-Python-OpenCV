# Image Stitching using Python and OpenCV

Image stitching is the process of combining multiple images with overlapping fields of view to create a panoramic or wide-angle image. This repository contains a Python script for image stitching using the OpenCV library.

## Requirements

- Python3
- NumPy
- OpenCV
- Imutils

## Library Installation

You can install the required dependencies using the following command:

```bash
pip3 install numpy
```
```bash
pip3 install opencv-python
```
```bash
pip3 install imutils
```

## Images Input

<div align="center">
  <div style="display:flex; flex-wrap:wrap;">
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/1.jpg" alt="1" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/2.jpg" alt="2" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/3.jpg" alt="3" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/4.jpg" alt="4" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/5.jpg" alt="5" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/6.jpg" alt="6" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/7.jpg" alt="7" width="200"/>
    <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-input/image1/8.jpg" alt="8" width="200"/>
  </div>
</div>


## Execute

```py
# import the necessary packages
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", type=str, required=True,
        help="path to input directory of images to stitch")
ap.add_argument("-o", "--output", type=str, required=True,
        help="path to the output image")
args = vars(ap.parse_args())

# grab the paths to the input images and initialize our images list
print("[INFO] loading images...")
imagePaths = sorted(list(paths.list_images(args["images"])))
images = []

# loop over the image paths, load each one, and add them to our
# images to stich list
for imagePath in imagePaths:
        image = cv2.imread(imagePath)
        images.append(image)

# initialize OpenCV's image sticher object and then perform the image
# stitching
print("[INFO] stitching images...")
stitcher = cv2.createStitcher() if imutils.is_cv3() else cv2.Stitcher_create()
(status, stitched) = stitcher.stitch(images)

# if the status is '0', then OpenCV successfully performed image
# stitching
if status == 0:
        # write the output stitched image to disk
        cv2.imwrite(args["output"], stitched)
        print("[INFO] Image stitched and saved to {}".format(args["output"]))

# otherwise the stitching failed, likely due to not enough keypoints)
# being detected
else:
        print("[INFO] image stitching failed ({})".format(status))
```

Execute this code using the following command:
```bash
python3 <image stitching file> --images <images input direcotry> --output <image output directory>/<output name.png>
```
For Example:
```bash
python3 image_stitching.py --images image-input/image1 --output image-output/image1/output.png
```
After the code has been executed, the output will be displayed:
```
[INFO] loading image...
[INFO] stitching images...
[INFO] Image stitched and saves to image-output/image1/output.png
```

And the output file will appear in the directory you specified in the command.

## Output
Here's the result:
<p align="center">
  <img src="https://github.com/NauvalPerdana/Image-Stitching-Python/blob/main/image-stitching/image-output/image1/output.png" alt="Your Image Description">
</p>
