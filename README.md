# Panorama-Maker

**Panorama-Maker** is a small project, the essence of which is to create panoramas. It was born when i recieved a large blade drawing for my diploma work, took photos of parts and decided to glue it all into one picture. So those photos of the drawing are used as a demonstration.

This project uses more than just built-in modules, please check the `requirements.txt` file.
```
pip install -r requirements.txt
```

Usage example:
```python
import cv2
import imutils
from panorama_maker import Stitcher

img_1_path = '.\Data\pan1.jpg'
img_2_path = '.\Data\pan2.jpg'
img_3_path = '.\Data\pan3.jpg'
img_4_path = '.\Data\pan4.jpg'
img_34_path = '.\Data\pan34.jpg'
img_234_path = '.\Data\pan234.jpg'
img_full_pan_path = '.\Data\pan1234.jpg'

path_list = [[img_3_path, img_4_path], 
             [img_2_path, img_34_path],
             [img_1_path, img_234_path]]

for i in range(len(path_list)):
    imageA = cv2.imread(path_list[i][0])
    imageB = cv2.imread(path_list[i][1])
    imageA = imutils.resize(imageA, height=3000)
    imageB = imutils.resize(imageB, height=3000)

    # stitch the images together to create a panorama
    stitcher = Stitcher()
    (result, vis) = stitcher.stitch([imageA, imageB], showMatches=True, ratio=0.75)
    if i == len(path_list) - 1:
        cv2.imwrite(img_full_pan_path, result)
    else:
        cv2.imwrite(path_list[i + 1][1], result)
```
Result:

<img src="Data/pan1234.jpg" alt="Drawing" width="1000"/>
