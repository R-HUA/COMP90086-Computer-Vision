# Convolutional neural networks  

<br> 

Typical architecture:  
- Some number of convolutional layers, with 
downsampling
- One or more fully-connected layers
- Softmax output with cross-entropy loss

Basic idea:
- Do feature embedding in convolutional layers 
(transform images from pixels to useful high-level 
features)
- Fully-connected layers are effectively a linear classifier 
(or MLP) to predict class from high-level features

<br> 

Image recognition
============

### Why is recognition difficult?
- Inter-category similarity
- Intra-category variability
    +  Instances
    + Illumination
    + Scale
    + Viewpoint/pose
    + Background/occlusion  
      
### Goal of image recognition
1. distinguishes different categories
2. but is invariant (or tolerant) to variation within a 
category  

<br> 

Convolutional layers
==============

+ Convolutions are defined by
    + A kernel, which is a matrix overlaid on the image and 
computes an element-wise product with the image 
pixels
    + A stride which defines how many positions in the image 
to advance the kernel on each iteration (stride = 1 
means the kernel will operate on every pixel of the 
image)  
<br> 

• Each neuron is connected 
to a small patch of the input  

• The neuron learns a 
convolutional kernel on the 
input  

• The output to the next layer 
is the input convolved with 
the neuron’s kernel 

+ Output size
    + Valid convolution (with kernel larger than 1x1) 
results in output smaller than input
    + If same-size output is needed, pad the input (zero 
padding is most common)  

<br>

• Each convolutional layer learns a set of kernels and 
outputs activation maps (= input convolved with learned kernel)

#### Advantages  
• Efficient – learns to recognize the same features 
anywhere in the image, with fewer parameters 
compared to fully-connected layer  
• Preserves spatial relations – output is an image with 
values indicating where features are present  

#### Disadvantages  
• Limited kernel size means model is limited to learning 
local features  

<br> 

Downsampling in CNNs
==============
- **Reduces output size** and number of computations 
needed in later layers ( more efficient in later layers)  
- Can also **improve tolerance** to translation –small 
changes in input won’t change downsampled
output  (increase translation invariance)  
<br>

### Strided convolution  

- no padding:

     **output_size = ceil((input_size - kernel_size + 1)/stride)**

- with padding 

    **output_size = ceil(input_size/stride)**  

<br>

• Advantage  

- Efficient – higher stride means fewer convolution 
operations  

• Disadvantage  

- Kernel window skips over parts of the image, so 
important image features could be missed

<br> 

### Max pooling

• After convolution, each activation map is separately 
downsampled  

• Max pool stride determines the amount of 
downsampling (output_size = input_size/stride)

•Advantage  
• Max pooling is most likely to preserve the most 
important features, compared to strided convolution or 
average pooling  

•Disadvantages  
• Average pooling “blurs” over features; important 
features may be lost  
• Pooling is slower than strided convolution

<br>

Regularisation in CNNs
==============
Regularisation is usually needed to reduce 
overfitting  

### L1, L2 regularisation
Adds an additional term to the loss function that 
encourages smaller values for the network 
parameters  

- #### Free parameters when adding regularisation:
    - How much weight to give regularisation term vs. other 
terms in the loss function
    - Which layers to include in regularisation –all layers or 
just later layers?
    - Which parameters to include –sometimes only weights 
are included, not biases  
- Adding regularisation tends to slow down training
- Too much regularisation can result in underfitting  

### Dropout

- Randomly discard some neurons (set output = 0)
- Forces neurons to find useful features 
independently of each other
- Effectively, trains multiple architectures in parallel


    • What percentage of neurons to drop is a free 
parameter (e.g., drop 50% or drop 20%)  
• Can be applied to all layers, or just later layers  
• Different dropout percentages can be applied to 
different layers –typically later layers would have more 
dropout  
• Adding dropout tends to slow down training  
• Dropout is onlyused in training –when evaluating 
the network on new data (validation/test), all 
neurons are active  

### Early stopping
•Stop training the network when it shows signs of 
overfitting  
- Monitor performance on a validation set
    -  Subset of data not seen in training and not included in 
test set
    - During training, periodically check model’s performance 
on the validation set –a decrease suggests overfitting

• Encourages smaller values for network parameters 
by keeping them close to their initial values (which 
are typically near 0)

 Loss functions
=========

### Softmax
Apply softmax function to last layer’s output  

Produces a vector that has the properties of a 
probability distribution:
- All values in range 0-1
- Values sum to 1

### Cross-entropy loss
Measure of the difference between the model and ground truth probability distributions

### ReLU
adds a non-linearity to the output of a convolutional kernel.   
allows for faster training of deep CNNs compared to other activation functions like sigmoid.  
helps reduce the vanishing gradient problem, compared to other activation functions.

<br>

Optimiser
==========
- Stochastic Gradient Descent (SGD)
- Root Mean Square Propagation (Rmsprop)
- Adaptive moment estimation (Adam)

<br>


Data preprocessing
====================
### Image whitening 
-  scale each image to 0-255 range, 
then normalise so each pixel has mean=0 and 
(optionally) std=1  

### Data augmentation
**Data augmentation is usually required to avoid overfitting**  

- Manipulate training data to generate more samples
- Without data augmentation, even smaller networks 
(e.g., AlexNet) overfit to ImageNet

- Common options:
    -  Random crops (e.g., 224 x 224 from 256 x 256 images)
    -  Horizontal reflection
    -  Small colour/contrast adjustments (to simulate different 
camera settings or times of day)
- Less common:
    -  Random rotation (e.g., +/- 15 degrees) slow
    -  Random scale <- slow
    -  Random occluders

### 


