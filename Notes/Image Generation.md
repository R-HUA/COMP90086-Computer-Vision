- **Discriminative** models
    - Learn conditional probability of class Y given attributes X: p(y|x)
    - produce a probability 
distribution over labels, given an image

- **Generative** models
    -  Learn joint probability of attributes X and class Y: p(x,y)
    - produce a probability 
distribution over images, given a label (conditional) 
or in general (unconditional)
    - Generative model contains discriminative model: 
you can use the joint probability to get p(y|x)
    - generative can do the reverse: p(x|y)


## Autoencoders

#### learns latent representation to reconstruct images

- Output of the network is whatever was passed to 
the network (e.g., an image)
- Hidden layer learns a lower-dimensional 
representation of the input
- No way to sample 
new data


### Hidden layer
- “Bottleneck” layer – smaller than the input
- Represents the input in terms of latent variables
- In the simplest case (one hidden layer with linear 
activation functions), this layer learns PCA

### Output and Loss
- Unlike a standard NN, the output is not a class or 
regression value – it’s the same type as the input 
(e.g., an image)
- Activation function is chosen appropriately:
    - For a binary image, tanh or sigmoid
    - For a regular image, linear activation
- Loss function = difference between input and 
output (e.g., MSE)

## Variational autoencoder (VAE)

#### probabilistic version of autoencoder, can sample from the latent space

- Loss function
    - Loss consists of two terms: reconstruction loss and 
regularisation loss
    - Reconstruction loss: encourages network to create 
output images as similar as possible to input 
images
    - Regularisation loss: encourages network to learn a 
latent representation z that is similar to the prior 
(standard normal distribution)

- Properties of the latent space
Properties of the latent space
    - To be useful for generation, the latent space should 
be:
    - Continuous: nearby points in the latent space 
correspond to similar images
    - Complete: every point in the latent space corresponds 
to a valid image
    - Standard normal distribution satisfies both of these 
requirements
    - Use of diagonal covariance matrices ensures latent 
variables are independent


- Advantages
    - Learns approximations of p(z|x) and p(x|z), where z is a 
latent variable representation of the input x
    - Can be used to generate new instances of x
- Disadvantages
    - Outputs often blurry 

## GAN

### GAN evaluation

GAN equilibrium does not necessarily mean the 
GAN has found a good solution


- Memorisation
- Realism
    - Inception score
        - Within a class, all images should be confidently 
classified with the correct label
        - Across classes, the GAN should produce a wide 
variety of confidently-classified images
- Diversity
    - Birthday paradox for GANs
        -   Suppose a generator that can produce 𝑁discrete 
outputs, all equally likely
        - Experiment: take a small sample of 𝑠outputs and 
count duplicates
            - The odds of observing duplicates in a sample of size 𝑠
can be used to compute 𝑁
            -   A sample of about  √𝑁 outputs is likely to contain at 
least one pair of duplicates    


### Conditional GANs

- Conditional GAN learns to sample p(x|y) (images 
conditional on y)
- If x-y pairs are available, can use the standard GAN 
architecture with additional input y
- If x-y pairs are not available, one option is 
CycleGAN – learns to transform samples from x->y 
and from y->x

