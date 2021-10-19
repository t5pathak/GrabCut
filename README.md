# GrabCut - Image Segmentation using MRFs

GrabCut is an image segmentation method based on graph cuts.

Starting with a user-specified bounding box around the object to be segmented, the algorithm estimates the color distribution of the target object and that of the background using a Gaussian mixture model. This is used to construct a Markov random field over the pixel labels, with an energy function that prefers connected regions having the same label, and running a graph cut based optimization to infer their values. As this estimate is likely to be more accurate than the original, taken from the bounding box, this two-step procedure is repeated until convergence. [Wikipedia](https://en.wikipedia.org/wiki/GrabCut)

At its core it's an iterative version of GraphCut. This methods was first introduced in the paper ["GrabCut” — Interactive Foreground Extraction using Iterated Graph Cuts](https://cvg.ethz.ch/teaching/cvl/2012/grabcut-siggraph04.pdf)

grabcut image in the middle

# Code Outline
The code below takes an input image and follows these steps:
- It requires a bounding box to be drawn by the user to roughly segment out the foreground pixels
- It runs an initial min-cut optimization using the provided annotation
- The result of this optimization gives an initial segmentation 
- To further refine this segmentation, the user provides two kinds of strokes to aid the optimization
    - strokes on the background pixels
    - strokes on the foreground pixels
- The algorithm now utilizes this to refine the original segmentation

# Image Segmentation - Result

### Effect of a tight initial bounding box or a loose bounding box
Tested for 2 different images and observed that a tighter bounding box was better at image segmentation especially at the boundaries. 
- Observe how the image segmentation is better towards the bottom of the banana. 

- Next, observe how the segmentation becomes better with a tighther bounding box

### Effect of a number of iterations
Tested for 2 different images and compared with different number of images. The initial bounding box was identical for both n=1 and n=5. 
- With the increase in iterations, notice how the segmentation boundary come closer to the real boundary. Pay attention to the boundary on top. As the number of iterations keep increasing we expect the segmentation to get even better.

- Similarly in this image of the bush the boundary gets tighter and tighter with increasing number of iterations.

### Changing the value of Gamma
Increasing the value of gamma made the segmentation process more aggressive. We altered the values of gamma for the same initial bounding box.

- Higher gamma has a more aggressive background seperation for the banana.

- Observe the same effect with the stone.


# Directory Structure
- ```src``` folder contains the source code. 
- ```img``` contains all the images to test the code on.
 
# Running the code
Any changes which need to be made, must be made in the code block under the heading "Main" only
1. Run the code which launches the GUI based environnment.
2. Draw a rectagle around the region to be kept using right mouse button.
3. Next you can mark refinment storkes - Mark with these keys 0 (background) and 1 (foreground).
