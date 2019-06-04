## [EfficientNet](https://arxiv.org/abs/1905.11946): Rethinking Model Scaling for Convolutional Neural Networks
> Authors: Mingxing Tan, Quoc V.Le. Notes by Lingkangjie, 2019-06-04

The authors use neural architecture search  method to design a new baseline network and scale it up to obtain family of models, called EfficientNets. This kind of ConvNets' design method is more automatic and accuracy in the feature. What is model scaling meaning? Model scaling is something that develops a fixed resource budget, basic module, and then scales them up for better accuracy, like ResNet-101 et al.

### Introduction
- In figure 1, the author show the relationship between number of parameters and Imagenet top 1 accuracy. Obviously, the less number of parameters of a network and higher top 1 accuracy indicates that the network is more efficient. Compared with the state-of-the-art network, EfficientNets achieves 8.4x smaller and 6.1x faster than GPipe on inference.
- the way to scale up ConvNets: by depth, or width, or image resolution, corresponding to image depth, width and image size.
- Traditionally, we scale the ConvNets only increase one dimension of network width, depth, or resolution. The authors propose a method called **compound scaling method** that uniformly scales all three dimensions with a fixed ratio. Specifically, the authors empirically show that if we want to use 2<sup>N</sup> times more computaional resources, then we can simply increase the network depth by alpha<sup>N</sup>, width by beta<sup>N</sup>, and image size by gamma<sup>N</sup>, where alpha, beta and gamma are constant coefficients determined by a small grid search on the original small model.
- one purpose of this work is that, since architecture search becomes increasingly popular in designing ConvNets, how to apply these techniques for larger models? The authors say, okay, we design a way to scale the baseline network to a super large ConvNets.
- Why we need to scale the depth, width and resolution of the network at the same time? Intuitively, if the input image is bigger, then the network needs more layers to increase the receptive field and more channels to capture more fine-grained patterns on the bigger image.

### Compound Model Scaling
1. The purpose of this paper is that trying to expand the network length, width, and/or resolution without changing pre-defined Conv operator in the baseline network. In order to reduce the design space, the authors restrict that all layers must be scaled uniformly with constant ratio.
2. Common way used by many ConvNets to design a larger network is scaling network depth. However, deeper networks are more difficult to train due to the vanishing gradient problem. Some techniques used to alleviate these problem, such as skip connections, batch normalization et al. Scaling network width is commonly used for small size models, as wider networks tend to be able to capture more fine-grained features and are easier to train. However, extremely wide but shallow networks tend to have difficulties in capturing higher level features. Higher resolution such as from 224x224 to 480x480, and to 600x600 also useful for improving accuracy. However, only scale the depth, or width, or resolution of the ConvNets, the accuracy gain quickly saturate after reaching 80%, demonstrating the limitation of single dimension scaling.
3. The authors observe that the resolution, width and depth of ConvNets are not isolated.It is critical to balance all dimensions of network width, depth and resolution during ConvNet scaling.

### EfficientNet Architecture
1. Since model scaling does not change layer operators in baseline network, having a good baseline network is also critical. So the authors design a new mobile-size baseline, called EfficientNet.
2. The paper search to optimize FLOPS rather than latency since it is not targeting any specific hardware device.
3. The main building block for the baseline network is [mobile inverted bottleneck](https://arxiv.org/pdf/1801.04381.pdf) MBConv coming from MobileNet. Table 1 tells us the architecture of baseline network called EfficientNet-B0.
4. How to scale EfficientNet? The authors define the scale factor of depth, width, and resolution for  ConvNet are alpha<sup>N</sup>, beta<sup>N</sup>, gamma<sup>N</sup> respectively. And alpha, beta, gamma are constrained to that `alpha * beta * beta * gamma * gamma` approximates to 2, and alpha, beta, gamma are must bigger than 1 or equal to 1.
5. **compound scaling method**: 
- step 1 is fix `N=1`, and use grid search to get the optimized alpha, beta, gamma. In baseline network EfficientNet-B0, the best values are alpha=1.2, beta=1.1, gamma=1.15.
- Step 2 is fix alpha, beta, gamma, scale up baseline network with different `N`.

In the paper, authors use EfficientNet-B0 with alpha=1.2, beta=1.1, gamma=1.15 as the best case of baseline and scale the network up with different `N`. Notice the final depth, width and resolution size for a network are alpha<sup>N</sup>, beta<sup></sup>, gamma<sup></sup> respectively.

6. At last, the EfficientNet achieve new state-of-the-art accuracy for 5 out of 8 datasets, with 9.6x fewer parameters on average. I notice that the results coming from EfficientNet are very approximate to other state-of-the-art models, meaning that of course EfficientNet is the best with less FLOPS also.
7. The paper also compares the scale only one dimension of network (by depth, by width, or by resolution) and its **compound scale** method, the result shows that its method can further improve accuracy. The model with compound scaling tends to focus on more relevant regions with more object details, while other models are either lack of object details or unable capture all objects in the images.

### Conclusion
- The proposed scaling method is simple but highly effective, which enables us to easily scale up a baseline ConvNet to any target resource constrains in a more principled way, whlie maintaining model efficiency.

