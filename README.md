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
<img width="500" alt="tb_1" src="https://user-images.githubusercontent.com/44245211/137881144-2daf9d11-16f8-4612-a563-6441144e54d0.png">
<img width="500" alt="lb_1" src="https://user-images.githubusercontent.com/44245211/137881165-4e1cc308-6d27-435f-8c5a-97ef54ea95a6.png">
- Next, observe how the segmentation becomes better with a tighther bounding box for the stone.
<img width="500" alt="tb_2" src="https://user-images.githubusercontent.com/44245211/137881172-80e940fd-5fb6-455a-b14e-5a88a83c26f6.png">
<img width="500" alt="lb_2" src="https://user-images.githubusercontent.com/44245211/137881177-2fbbbe95-8ce2-45a9-8d6f-eaf55f310ea6.png">

### Effect of a number of iterations
Tested for 2 different images and compared with different number of images. The initial bounding box was identical for both n=1 and n=5. 
- With the increase in iterations, notice how the segmentation boundary come closer to the real boundary. Pay attention to the boundary on top. As the number of iterations keep increasing we expect the segmentation to get even better.
<img width="500" alt="n_1" src="https://user-images.githubusercontent.com/44245211/137881180-c8bbe1db-d122-40cb-acfa-d9113cc31bb6.png">
- Similarly in this image of the bush the boundary gets tighter and tighter with increasing number of iterations.
<img width="400" alt="n_2" src="https://user-images.githubusercontent.com/44245211/137881183-c77ffa46-5bb1-407b-8b39-5cf260bffe2a.png">

### Changing the value of Gamma
Increasing the value of gamma made the segmentation process more aggressive. We altered the values of gamma for the same initial bounding box.
- Higher gamma has a more aggressive background seperation for the banana.
<img width="500" alt="g_1" src="https://user-images.githubusercontent.com/44245211/137881185-a4364141-4644-4e95-8cb9-75caa90d719f.png">
- Observe the same effect with the stone.
<img width="500" alt="g_2" src="https://user-images.githubusercontent.com/44245211/137881187-74e0ca77-842c-4887-ab84-893df2924d71.png">

# Directory Structure
- ```src``` folder contains the source code. 
- ```img``` contains all the images to test the code on.
 
# Running the code
Any changes which need to be made, must be made in the code block under the heading "Main" only
1. Run the code which launches the GUI based environnment.
2. Draw a rectagle around the region to be kept using right mouse button.
3. Next you can mark refinment storkes - Mark with these keys 0 (background) and 1 (foreground).
