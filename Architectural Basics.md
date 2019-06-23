# ARCHITECTURAL BASICS

The order to consider for designing deep networks' architecture - <br/>
1. **Receptive field** - Before designing the architecture, we first need to look at the images that the network needs to operate on. The network should be deep/wide enough to capture the required receptive field, which is equal to the sizes of the object in the image that are to be classified. The size of objects are not limited by the image size, viz if the image is only a part of the object.
2. **Number of layers** - The number of layers are decided based on the required receptive field to classify objects. 
3. **3x3 convolutions** - These convolutions are used to achieve the requisite receptive field as multiple 3x3 convolutions can be used to achieve the same local receptive field as higher convolutions, with lesser parameters.
4. Softmax
5. Initial epochs for how well network is training 
6. Kernels and their number
7. Max Pooling 
8. Position of max pooling
9. Max pooling distance from prediction
10. 1x1 convolutions
11. Transitions layers
12. Position of transition layers
13. Image Normalization
14. Batch Normalization
15. Distance of batch normalization from prediction
16. Number of epochs and increasing them if training accuracy has not converged.
17. Checking accuracy on validation data for every epoch
18. Dropout when the network is overfitting (difference between training and validation accuracies is large)
19. Batch Size
20. Learning rate
21. Adam or SGD
22. LR Scheduler




When do we stop convolutions and go ahead with a larger kernel or some other alternative (which we have not yet covered)
etc (you can add more if we missed it here)

