---
title: "So You Want to Segment a Cell?"
layout: post
date: 2017-05-01
tag:
- science
- imaging
- microscopy
- image analysis
blog: true
---

# What is segmentation?

Segmentation is the act of discriminating foreground from background in an image or separating distinct regions.

In biological image analysis, this often distills down to discriminating objects or regions of interest like cells from uninteresting regions, like debris or background.

Segmentation is often one of the first steps in an image based cytometry pipeline. Before you can analyze a cell's morphology, you need to find the cells in your image. For the rest of this post, I'll demonstrate how to segment a brightfield cell image as an exercise for learning basic segmentation techniques.

# What separates foreground from background?

Taking a step back, let's think abstractly about how we determine whether a given region of an image is foreground or background -- in this case, cell or plastic. It seems trivial because our brains perform recognition unconsciously, but if you focus you can describe the particular qualities that separate an apple from a fruit bowl, a child from a field of grass, or yes, a cell from plastic.

If we consider some of the qualities for our special case here, we might say that cells in brightfield images are darker than their background, with more diverse textures, and with specific shapes or structures inside. Imagine going pixel-by-pixel through an image and measuring how much of each of these qualities the pixel exhibits -- darkness, texture relative to neighboring pixels, the presence of particular shapes. We could create a companion images of equal size for each of these qualities, where each pixel's intensity represents not the number of photons captured by the detector, but our measurement of that particular quality.

These "companion images" are known as **response maps** or **feature maps**. They are often generated by [**convolving**](https://www.wikiwand.com/en/Convolution) a **filter** that measures some desired property, and the resulting output is known as the **response** to the filter. Filtering to measure these properties of interest will be one of three primary tools we use for segmentation.

Let's take a tour of those tools.

## (1) Thresholding

Once we have a response map that tells us which sections of the image are more textured, which contain certain shapes, etc, how do we go about finding a cut-off for the foreground relative to the background?

Enter, thresholding.

Thresholding algorithms attempt to set a cut-off separating two modes of a distribution. What's the simplest thresholding algorithm we can imagine? We could take the mean $\mu$ of the distribution of values $X$ in our response map and then simply classify values above the mean as foreground and values below as background. Such a simple algorithm doesn't work very well in practice, but it gives you an idea for how thresholding works. Applying such an algorithm to the whole set of pixels in an image $X$ is known as **global thresholding**. As one might guess, there is also a concept of **local thresholding**, where thresholding algorithms are applied in the same manner, but considering subsets of pixels at a time in a series of "neighborhoods."

The most common thresholding algorithm in image processing is [Otsu's algorithm](https://www.wikiwand.com/en/Otsu's_method) applied globally, which minimizes the variance within the "classes" you're separating, and maximizes the variance between them. Otsu's method is implemented in most common image processing toolboxes, including in Matlab as `graythresh` and in Python's `scikit-image` as `skimage.filters.threshold_otsu`. Several other thresholding algorithms exist and have common implementations. The `scikit-image` documentation has a [nice overview](http://scikit-image.org/docs/dev/auto_examples/segmentation/plot_thresholding.html#sphx-glr-auto-examples-segmentation-plot-thresholding-py).

## (2) Filtering

In order to generate response maps for features other than simple brightness, we need to find a mathematical way of measuring our features of interest. As mentioned above, convolving an image with a specific [filter kernel](https://www.wikiwand.com/en/Kernel_(image_processing)) will generate a response map, so all we need to do is find a set of filter kernels that measure properties we're interested in!

Understanding the mathematics behind two-dimensional convolution is really critical to understanding image processing, and I highly recommend reading up on the topic if you're unfamiliar. Cornell's CS Dept. has a [nice tutorial](http://www.cs.cornell.edu/courses/cs1114/2013sp/sections/S06_convolution.pdf) and a [live visual demonstration](http://setosa.io/ev/image-kernels/) is available from Victor Powell.

### Features of interest

Listed here are some common filters used for different features of interest in simple segmentation problems. There are many more, and each of these filters has multiple uses, but this list is a basic toolkit to help us get started.

Feature | Kernel
----------|--------------------
Blobs | [Laplacian of Gaussian](https://www.wikiwand.com/en/Blob_detection)
Brightness | N/A | N/A
Edges | [Canny](https://www.wikiwand.com/en/Canny_edge_detector)
Edges | [Sobel](https://www.wikiwand.com/en/Sobel_operator)
Edges | [Gradient of Gaussian](https://www.wikiwand.com/en/Edge_detection)
Texture | Combinations of Edge Filters

## (3) Morphological Operators

In addition to convolutions (i.e. filtering) and thresholding, morphological operators are the third leg of the stool that enables accurate segmentation.

At the most basic level, a morphological operation considers each pixel in an image and applies a non-linear transformation based on some rule. These rules usually consider some neighborhood of pixels around the center pixel, and apply a transform based on pixels in the neighborhood. The most common morphological operations are called **dilation** and **erosion**. We'll walk through the details of each below.

### Structuring Elements

How do we decide what the "neighborhood" around each pixel we're transforming is? We use structuring elements.

[Structuring elements](https://en.wikipedia.org/wiki/Structuring_element) are essentially shapes encoded as a binary matrix. So, if we want the neighborhood for morphological operation to be a disk with a radius $r$, we can generate a structuring element matrix that encodes a circle of `True` pixels. Using this disk structuring element, we can apply some transformation to each pixel in the image based on the neighboring pixels within the disk centered on the pixel to be transformed.

Example 1 -- Disk structuring element for $r = 3$

![Disk structuring element]( {{ site.url }}/assets/images/segment_a_cell/disk_se.png)

Example 2 -- Square structuring element for $h = 3$

![Square structuring element]

### Dilation

[Dilation](https://en.wikipedia.org/wiki/Dilation_(morphology)) considers each pixel in an image and sets the value of this pixel to the *maximum* value of all pixels in a specified neighborhood. You can think of it sort of like a non-linear filter that applies a $\max$ operator rather than a convolution. So, it will set the value of each pixel to the highest pixel value within the neighborhood.

Whereas convolution is denoted with a $\star$, dilation is denoted with the operator $\oplus$. Mathematically, we denote the dilation of image matrix $I$ by structuring element $S$ as:

$$I \oplus S = \bigcup_{s \in S} I_s$$

where $\bigcup$ is the union operator, denoting that our final dilated image is the union of structuring element sized "subimages" where I is transformed by the $\max$ operator with $S$. This can be intuitively understood as saying that the value of each pixel in the new transformed image is set based on the $\max$ value in the pixel's neighborhood in the *original* image, i.e. we don't transform part of the image "in place", then consider those new transformed values for the next pixel over. Think of it like we make an empty copy of the image matrix, then fill it in pixel by pixel considering only the pixels of the original image.

What does dilation look like in practice?
Here, we perform dilation on a single pixel at the center of an image using a disk structuring element. You'll see we create a disk! This makes intuitive sense, as when we scan across the image and perform the $\max$ operation

[Example images]

### Erosion

Now that we understand dilation, understanding erosion is easy.

[Erosion]() considers each pixel in image and sets each pixel to the *minimum* value of all pixels in a neighborhood. Just like dilation, but instead of taking the $\max$ we're taking the $\min$.

We can see how this works when we erode the images we just dilated.

[Example images]


### Opening and Closing

It can be useful to perform a dilation followed by a corresponding erosion, and vice-versa. At first this seems a bit counterintuitive. Why perform two operations that leave us close to the starting point?

Eroding an image followed by a corresponding dilation (i.e. a dilation of similar magnitude and shape) is known as **opening**. This name comes from the fact that eroding tends to break thin "bridges" between binary objects. The subsequent dilation returns objects to roughly the same size as the starting point, but doesn't restore these bridges, unlinking connected objects. You can think of it like "opening" a drawbridge linking two binary land masses.

Conversely, dilating an image followed by a corresponding erosion is known as **closing**. Two binary objects that are separated by a thin margin may form a connecting bridge when dilated, and the subsequent erosion may not break this bridge if it is thick enough. This "closes" the gaps between two objects.

As may be obvious, these dilation/erosion combinations are useful when you're trying to separate touching cells, or connect parts of the same cell that might initially be separated in your segmentation.

In grayscale images, the same intuitions apply. Just think of opening as removing small high intensity connections between larger high intensity areas, and vice-versa for closing.

[Example images]


# Segmenting a Cell Image

Here's our challenge: create a binary "mask" that labels pixels representing a cell as $1$ and pixels labeling background as $0$ in this image.

[img placeholder]

When we're done, we'll have a mask that looks like this.

[mask placeholder]

As you can see, it separates cells from the background quite nicely.

[overlay placeholder]

## Considering Brightness