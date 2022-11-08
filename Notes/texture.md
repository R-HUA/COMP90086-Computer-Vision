# Texture


- A definition from image processing:  

    Texture is an region with **spatial stationarity** (same statistical properties everywhere in the region)

- A definition from computer graphics:  

    Texture is a 2D surface applied to a 3D model  


### Types:
- Periodic texture &emsp;  周期性纹理
- Stochastic (aperiodic) texture  &emsp;   随机（非周期性）纹理

### Texture models

- Parametric models &emsp;  参数模型: 

    Represent texture with a set of adjustable parameters


- Non-parametric (stitching) models &emsp;  非参数（拼接）模型: 
 
    Represent texture as image patches &emsp;  将纹理表示为图像补丁  

<br><br>

Texture synthesis
-------------------
### Non-parametric texture synthesis
1. Randomly sample a small (e.g., 3 x 3 pixel) patch from the 
original image
2. Spiral outward, filling in missing pixels by finding similar 
neighborhoods in the original texture
(Neighbourhood size is a free parameter that specifies how 
stochastic the texture is)  

### Image quilting

 Use existing patches of texture to synthesis more 
texture; main problem is connecting them together 
**without visible artefacts/seams**  

 “Corrupt Professor’s Algorithm”
- Plagiarize as much of the source image as you can
- Then try to cover up the evidence

<br>

#### • Choose patch and overlap size    

#### • Initialize with a random patch    

#### • For each subsequent patch:  
+ Find a patch in the original texture 
that is most similar to this region, 
considering only the pixels in the 
**overlap region**  
- Seamlessly paste in patch by cutting 
along a path with minimum overlap 
error  

<br>
<br>

## Image inpainting

- Similar idea to fill in missing regions of an image:
    -  Find a similar patch in anotherimage
    - Paste in patch with an error-minimizing cut

<br>
<br>

## Parametric texture synthesis

- Fourier texture synthesis
    - Synthesize texture by matching Fourier magnitude
    - Okay results for some simple textures, but doesn’t 
work well in general


<br>
<br>

-------
- Non-parametric texture synthesis is based on 
copying texture patches
    -  Works very well on periodic textures
    -  Disadvantage: No model of texture parameters
- Parametric texture synthesis represents textures in 
terms of a set of parameters
    -  Most methods work better on stochastic textures
    -  Disadvantage: Even very complex models (e.g., based on 
neural networks) may be incomplete


<br>
<br>

## Texture transfer
•Texture transfer –render an image in the style of 
another image  
•Image content represented by neural network 
responses  
•Texture represented by correlations of feature 
maps across multiple layers of a neural network






