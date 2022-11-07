### Cues for depth
2D images contain a variety of information for 
depth perception  

- Perspective
- Texture
- Object position and occlusion
- Object knowledge
- Binocular stereo
- Motion parallax

<br>

# Stereo

It is possible to compute depth from single images, 
but more accurate depth measurements can be 
obtained from multiple views (e.g., stereo)

<br>

### Depth from stereo
Stereo depth is computed from disparity 
(difference in position of points in two views of a 
scene)  

z/B = f / (x - x')  

### stereo matching
- SSD
- NCC

### Effect of window size

- Smaller window = finer detail, but more noise
- Larger window = smoother depth, but lacking detail

### Match failures
- Reflective object
- Painted object

### Additional constraints

- Uniqueness: a point in one view has no more than one 
match in the other view
- Ordering: corresponding points should be in the same 
order in both views
- Smoothness: disparity values should change smoothly 
(for the most part)  

<br>

>    ### What if the image planes are not parallel?  
>
>    Rectification finds projective transform that maps each image to the same plane

<br>

# Single-view depth

### Supervised depth classification

- Treat depth estimation as a classification task: For 
each pixel in image, predict distance from camera
- Train on images with annotated depth maps
  
  <br>

- Images may have a very large range of depths – a 
loss based on log(depth) may work better than 
absolute depth
- Mean depth of scenes can vary widely (e.g., closet 
vs. stadium). To discourage models from simply 
learning mean depth, consider scaling the loss 
function so that it is similar for different scenes.


### Depth from disparity
Instead of training on annotated depth maps, train 
on stereo image pairs  

Advantage:   
stereo image pairs can be produced 
with standard cameras, while depth maps require 
special equipment (e.g., LiDAR)

Disadvantages:  
"Blurry" depth at object edges (but can be combined 
with edge maps for better results)  
Models may not generalise well to new contexts  



- Input: one image from a stereo pair (e.g., left)
- Learn to predict the disparity map that will produce 
the other image (e.g., right)
- Distance from camera to surfaces can be computed 
from the disparity map
- Train on stereo pairs

- Loss is sum of:
    - Appearance loss 
(difference between 
original and 
predicted image)
   - Disparity 
smoothness loss
   - Left-right 
consistency loss 
(difference between 
disparity maps)
