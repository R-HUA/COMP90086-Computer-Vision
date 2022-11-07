# Filters

>#### Pixel operator: 
>   - transform pixel based on its value

>#### Local operator: 
>   - transform pixel based on its neighbours

>### Linear filtering
>
>   Cross-correlation  
>   Convolution
>
> 深度学习里的卷积(convolution)则是建立在cross-correlation基础上的
>
>#### Common filters
>   * Average/blur filters: average pixel values, blur the image
>       + Box filter
>       + Gaussian filter
>   * Sharpening filters: subtract pixel from surround, increase fine detail
>   * Edge filters: compute difference between pixels, detect oriented edges in image
>       + Sobel operator
>
> #### Properties of linear filters
> + f * h = h * f
> + (f * h1) * h2 = f * (h1 * h2)
> + f * (h1 + h2) = (f * h1) + (f * h2)
> + kf * h = f * kh = k(f * h)
>
> #### Border handling
> At border pixels, the convolutional kernel will extend beyond the border of the image. 
> +  Pad with constant value
>+  Wrap image
>+ Clamp / replicate the border value
>+ Reflect image
>   
>Wrap is ideal for tiling textures (but not photos)  
>Clamp/replicate tends to work well for photos
>
>• Linear filters: first step of almost all computer vision systems  
>• Linear filters are just a first step –you can’t build 
complex feature detectors from just linear filters
>
> <br>

<br><br><br>

# Fourier transform
Fourier transform decomposes signal into 
component frequencies  
Time domain -> frequency domain (or, for images, 
spatial domain -> frequency domain)  

- Fourier analysis of images  
    +  Any image can be represented by its Fourier 
transform
    + Fourier transform = for each frequency, magnitude 
(amplitude) + phase
    + Magnitude captures the holistic “texture” of an 
image, but the edges are mainly represented by 
Fourier phase

### Operations in frequency domain  
Frequency domain is a convenient space for many 
applications  

Convolution in spatial domain = multiplication in 
frequency domain or the frequency domain
- Bandpass filter   
a filter that removes a range of 
frequencies from a signal
    + Low pass filter
    + High pass filter

#### Applications
- Image compression  
• Frequency domain is a convenient space for image 
compression  
• Human visual system is not very sensitive to 
contrast in high spatial frequencies  
• Discarding information in high spatial frequencies 
doesn’t change the “look” of an image

- Image forensics

   
<br><br><br>

# Colour

### SPD 
    Spectral power distribution  光谱功率分布  

#### Perceived colour   
    Most surfaces reflect a range of wavelengths, but perceived colour is a function of cone response

    ->  Many different spectra appear to be the same colour  

The RGB responses are based on the integral of the camera's sensor sensitivity curve times the SPD, so the shape of the SPD could be different for each object but integrate to the same value. This is why the same colour can be perceived from different spectra.


• Many trichromatic colour spaces  
• RGB most common for image storage, other spaces 
may be more useful for colour manipulations

<br>  


# Shading and surfaces

- Recovering surface shape and reflectance from a single image is difficult  
- Generally requires additional assumptions or constraints:
    + Assumptions about surface (e.g., matte, smooth)
    + Shape and/or lighting priors
    + Images contain a lot of information, and it’s not easy to separate out sources

<br><br><br>

# Edges
## Edge detection
Edge detection is the first step for most visual 
processing systems  

* Causes of edges
     + surface normal discontinuity  
     + depth discontinuity  
     + surface color discontinuity   
     + illumination discontinuity  

### Gradient
+ Edges are points in the image with a high change in intensity = high change in gradient
#### Edge detector  
Accurate edge detection requires smoothing image 
noise  
Partial derivatives in x, y  
Edge filter: Sobel  
Edge detector = derivative of Gaussian filter, 
combines smoothing and gradient response

## Canny edge detection
•Defines edges based on image gradient  
•Post-processing of gradient to better localise edges 
(non-maximum suppression) and preserve 
faint/broken edges (thresholding with hysteresis)

+ Non-maximum suppression 非极大值抑制
+ Thresholding with hysteresis
    + Two thresholds T1, T2 with T1 > T2
    + Strong edges: magnitude > T1
    + Weak edges: T1 > magnitude > T2
    + For each weak edge:
        + Check the 8-pixel neighbourhood around this pixel
        + If any neighbour is a strong edge, relabel the weak edge pixel as a strong edge
    + Final edge map = strong edges
<br>
   
## Edges for image recognition
Edge-based features have desirable properties for visual recognition
+ Compression
    + Edge = discontinuity
    + Efficient way to represent images: only represent points where the signal changes
+ Invariance
    + Edge-based features are invariant or tolerant to many irrelevant image changes