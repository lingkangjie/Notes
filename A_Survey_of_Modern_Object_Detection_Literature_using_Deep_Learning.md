## A Survey of Modern Object Detection Literature using Deep Learning
> Karanbir Chahal and Kuntal Dey, 2018
> Notes by Ling Kangjie

### Meta knowledge
- Object detection is the identification of an object in an image along with its localization and classification.
- The single step approach classifies objects in images along with their locations in a single step, while the two step approach separates the detection task into the region proposal step and object detection step.
- The RCNN model takes every region proposal and runs them through the convolutional base. Fast RCNN aims to reduce this overhead by running the convolutional base just once. It runs the convolutional base over the entire image to generate a feature map. The regions are cropped from this feature map instead of the input image. The major innovation of Fast RCNN was in sharing the features of a convolutional net.
- Fast RCNN using ROI Pooling to takes the coordinates of regions obtained via the Selective Search and directly crops it out from the convoluted feature map.
- Firstly, Fast RCNN shares computation through the ROI Pooing step. Secondly, it introduces a simpler single step training pipeline and a new loss function.
- Faster RCNN introduced the *Region Proposal Network (RPN)* to replace Selective Search.
- Feature Pyramid Network (FPN) are designed to represent the image at different scales. The regression and classification heads are run across these multi scale feature maps. Anchors represent various aspect ratios instead of scale.
