# Count Dots In An Image

This uses code from https://stackoverflow.com/questions/38619382/how-to-count-objects-in-image-using-python to count dots in an image. 

##

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

