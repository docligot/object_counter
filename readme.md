# Count Objects In An Image

These code snippets allow counting of objects in an image. 

## Use-case: Counting Dots

Original image: 

![Alt text](https://github.com/docligot/object_counter/blob/main/dots.png)

```
from skimage import io, filters
from scipy import ndimage
import matplotlib.pyplot as plt

im = io.imread('ba3g0.jpg', as_grey=True)
val = filters.threshold_otsu(im)
drops = ndimage.binary_fill_holes(im < val)
plt.imshow(drops, cmap='gray')
plt.show()
```

Will render the image as: 

![Alt text](https://github.com/docligot/object_counter/blob/main/bw_dots.png)

Then to count: 

```
from skimage import measure
labels = measure.label(drops)
print(labels.max())

# 96
```

## Use case: Count contours

Original Image: 

![Alt text](https://github.com/docligot/object_counter/blob/main/containers.png)

```
import cv2
image= cv2.imread('containers.png')
gray= cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
edges= cv2.Canny(gray, 50, 200)
_, contours, _= cv2.findContours(edges.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
number_of_objects_in_image= len(contours)
print ("The number of objects in this image: ", str(number_of_objects_in_image))

# The number of objects in this image:  4

```

## References

Counting Dots: https://stackoverflow.com/questions/38619382/how-to-count-objects-in-image-using-python 
Counting Containers: http://www.learningaboutelectronics.com/Articles/How-to-count-the-number-of-objects-in-an-image-Python-OpenCV.php