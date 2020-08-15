# CNN Image Classifiers
This Repository consists of my custom CNN Classifiers notebooks

## CIFAR10 Classifier
Using CNN Classified CIFAR10 dataset

## MNIST CLassifier

Achieved an Accuracy of 99.5% with
<ul>
  <li>less than 20,000 parameters</li>
  <li>Training using less than 20 epochs</li>
  <li>Reached 99% in less than 10 epochs</li>
  <li>Without using a Fully connected Layer</li>  
</ul>


## Highlights
<ul>
  <li>Trained with less than 20000 parameters</li>
  <li>Achieved a Test accuracy of greater than 99.4% in less than 20 epochs</li>
</ul>

## Model Construction (MNIST Classifier Model Using Dropout)

#### Model Definition
While constructing the model, a few techniques were used to surpass our goal of 99.4% validation accuracy. Our model contains 2 blocks with a transition layer in between. 

<ul>
<li> <p><b>Batch Normalization</b></p>
<p>We apply Batch normalization at every layer to normalize the inputs to the next layer. </p>
</li>
<li> <p><b>Drop-out</b></p>
<p>We apply drop out after batchnorm every time to regularize our input and to prevent our model from overfitting.</p>
</li>
<li> <p><b>Max Pooling</b></p>
<p>Max pooling was applied after we reached a receptive field of 7. At this point, the model captures lines / edges, curves in its entirety and can now combine features into higher level objects. </p>
</li>
<li> <p><b>1x1 Convolution</b></p>
<p>Together with the Max Pooling layer, this makes up our transition layer. This is primarily to reduce the number of channels while effectively combining features from all channels.  </p>
</li>
<li> <p><b>Global Average Pooling</b></p>
<p>This layer is introduced when our channel dimension is 5x5. Not only does this translate convolutional structure to linear structure, it has the added advantage of having less parameters to compute and since it doesn't have to learn anything, it helps avoid overfitting. This is a sort of transition layer. </p>
</li>

</ul>

<p align="center"> <strong>CONV2D_1 -> 28 x 28 x 1  || (3x3x1) x16  || 26 x 26 x 16  </strong> </p>
<p align="center"> <strong>CONV2D_2 -> 26 x 26 x 16 || (3x3x16) x16 || 24 x 24 x 16   </strong> </p>
<p align="center"> <strong>CONV2D_3 -> 24 x 24 x 16 || (3x3x16) x32 || 22 x 22 x 32    </strong> </p>
<p align="center" >TRANSITION LAYER (Minimum Receptive for feature detection has reached)<p>
In Transition layers we are combining the simple features we have extracted in previous convolutions to make complex features/Textures/patterns
<p align="center"> <strong>22x22x32 || (1x1x32)x16 || 22x22x16 </strong> </p>
<p align="center" >Pooling Layer<p>
<p align="center"> <strong> Pool_1 -> 22 x 22 x 16 || MaxPool( 2x2 ) || 11 x 11 x 16</strong> </p>
<p align="center" >CONVOLUTION BLOCK 2<p>
<p align="center"> <strong> 11 x 11 x 16 || (3 x 3 x 16) x 16 || 9 x 9 x 16 </strong> </p>
<p align="center" >Layer with padding 1 <p>
<p align="center"> <strong> 9 x 9 x 16 || (3 x 3 x 16) x 16 || 9 x 9 x 16  </strong> </p>
<p align="center"> <strong> 9 x 9 x 16 || (3 x 3 x 16) x 16 || 7 x 7 x 16</strong> </p>
<p align="center"> <strong> 7 x 7 x16 || (3 x 3 x 16) x 32 || 5 x 5 x 32</strong> </p>
<p align="center" >Final Block <p>
<p align="center"> <strong> 5 x 5 x 32 || (1 x 1  x 32) x 10 || 5 x 5 x 10 </strong> </p>
<p align="center">  Global averge Pooling </p>
<p align="center"> <strong> Output = 1 x 1 x 10 </strong> </p>

#### Data Augmentation
<p>The input images were randomly rotated by 10 degress to introduce slightly more variance and have the model generalize better. </p>

<p align="center" >transforms.RandomRotation(10)<p>

<p>Input data was also normalized with the mean and standard deviation of the input dataset. </p>

<p align="center" >transforms.Normalize((0.1307,), (0.3081,))<p>

#### Conclusion
We crossed our target of 99.4% even before we completed 20 epochs. The max validation accuracy went upto 99.5%. All this while keeping our total number of parameters less than 20000. 
