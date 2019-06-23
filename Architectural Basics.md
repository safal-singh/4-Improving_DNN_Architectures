# ARCHITECTURAL BASICS

The order to consider for designing deep networks' architecture - <br/>
1. **Receptive field** - Before designing the architecture, we first need to look at the images that the network needs to operate on. The network should be deep/wide enough to capture the required receptive field, which is equal to the sizes of the object in the image that are to be classified. The size of objects are not limited by the image size, viz if the image is only a part of the object.
2. **Number of layers** - The number of layers are decided based on the required receptive field to classify objects. 
3. **3x3 convolutions** - These convolutions are used to achieve the requisite receptive field as multiple 3x3 convolutions can be used to achieve the same local receptive field as higher convolutions, with lesser parameters.
4. **Softmax** - The output from the convolutions in the network is converted to percentage for each of the classes using the softmax activation function. It pushes values to 0 or 1 given the residual after convolutions. 
5. **Initial epochs for how well network is training** - Check the training and validation accuracies of the first ~4 epochs of the network to compare its performance with the baseline network. 
6. **Kernels and their number** - Kernels act as feature extractors, with their values (or the feature which they search for) being determined by backpropagation. The kernels in a block (the layers between 2 transition layers) are increased to be able to capture the different combinations of features that were extracted by kernels in the previous layer.
7. **Max Pooling** - If only convolutions are used, the number of layers can be very high, given the large image sizes. Therefore, max pooling layers are incorporated to aggregate the information and multiple-fold the receptive field captured yet (with some information loss) by letting strong activations pass through as well as reduce the number of layers required to reach receptive field.  
8. **Position of max pooling** - Any image comprises of features- **edges and gradients, textures, patterns, parts of object, object and the scene**- and these image features are captured in the given order by the network. Every block with multiple convolution layers (the number of layers required to reach the receptive field needed to capture the feature, viz 11x11 for 200-400 pixel images) is separated by max-pooling layers, which aggregate the information and increase the receptive field multiple folds.
9. **Max pooling distance from prediction** - Max pooling increases the receptive field multi-folds but it also leads to loss of information, which cannot be afforded near the prediction layer as each pixel remaining near the prediction layer consists of high information crucial for classification. Therefore, max-pooling layers are placed ~2-3 layers apart from the prediction layer.
10. **1x1 convolutions** - The number of channels are downsized before beginning convolution blocks, as a block extracts a particular feature (**edges and gradients, textures, patterns,...**) of the image. If 1x1 convolutions are used for downsizing followed by 3x3 for convolution, the  number of parameters would be much lower than that required for simultaneous downsizing and convolution using a single 3x3 convolution. eg. <br/>
For downsizing image channels from 256 to 64, for 1x1 followed by 3x3:<br/
Number of parameters = 1x1x256x64 + 3x3x64x64 = 53248 <br/>
For downsizing and convolution using just 3x3:<br/>
Number of parameters = 3x3x256x64 = 147456<br/>
Ratio = 147456/53248 = 2.77<br/>
It can be seen that not using 1x1 convolutions costs us 2.77 times more parameters. Note - No bias has been taken for calculations.
11. **Transitions layers** - 1x1 convolutions followed by Max pooling is called transition layer. Here, 1x1 reduces the number of channels for the next block while max pooling multi-folds the receptive field to be able to capture the next feature (edges and gradients-> textures-> patterns...), as the following features are identified by looking at a bigger receptive field.
12. **Position of transition layers** - Transition layers are placed between blocks of convolutions that capture a particular image feature. It should be ~2-3 convolutions away from the prediction layer.
13. **Image Normalization** - It ensures that all images have their pixel values in the same range, so that the network is agnostic to the image brightness. The pixel intensities are translated such that their distribution remains the same.
14. **Batch Normalization** - It normalizes the pixel values of image channels of a layer in the network, with each channels having its respective mean and variance. Therefore, it helps in reducing the variation in the convolution inputs to intermediate layers of network and hence, generalize better to different pixel values of input image.  
15. **Distance of batch normalization from prediction** - In the prediction layer, the values of different channels are used to infer the class of object in the input image, with strong activation from different sets of channels helping to identify each class. If batch normalization is applied to the prediction layer, the means and variances learnt for normalizing from images of different classes will lessen the activation for some classes, resulting in wrong outputs. Therefore, batch normalization is not applied to the prediction layer. 
16. **Checking accuracy on validation data for every epoch** - Helps to identify if the model is over/underfitting
17. **Number of epochs** - The number of epochs are increased if the training accuracy has not converged. 
18. **Dropout** - Used when the network is overfitting (difference between training and validation accuracies is large).
19. **Batch Size** - Increase in the batch size helps in generalizing the model better and avoiding local minima.
20. **Learning rate** 
21. **Adam or SGD**
22. **LR Scheduler** - Scheduling the change of learning rate with each epoch to avoid getting into local minima and ensuring convergence (large learning rates will not lead to convergence).
23. **Different convolutions** - In case normal 3x3 convolutions are not able to capture the image features, convolution like dilated kernels, grouped convolutions, skip connections, etc are used.
