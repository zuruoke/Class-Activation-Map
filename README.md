# Class-Activation-Map

## MOTIVATION:
This technique allows re-using classifiers for getting good localization results even when training without bounding box coordinates data
You don't need to draw a box, simply train a classifier - you can automatically know where the object is.


*Class activation maps* are a simple technique to get the discriminative image regions used by a CNN to identify a specific class in the image. 
In other words, a class activation map (CAM) lets us see which regions in the image were relevant to this class  
The corresponding weights of the feature vector connected to the logistic regression aids to weight the importance of each object in the image in relation to a classification of a particular image. 

*In this kernel*, I used this workflow to get my Class Activation Map:

- *Load a Resnet50* pretrained on Imagenet but cut it off at the last activation layer, which returns 2048 7x7 feature maps of the query image 

- *Use the Resnet50* model to predict the class of the query image

- *With the class of the query image*, take the corresponding weights of the logistic regression, i.e the last dense layer weights

- *Compute the dot product* of the 2048 7x7 feature maps and the logistic regression weights of the query image class, returns 7x7 image

- *Upsample the 7x7 image* to the original size of the image using scipy

- *Overlay a sort of heatmap* over the query image

- *Plot* both the query image and its overlayed heatmap constituent  

N/B: The area around the main object which the network presumes is relevant for it's prediction is hotter than the rest, hence the name, "heatmap"


## CONCLUSION:
- This also shows how deep learning networks already have some kind of a built in attention mechanism.

- This should be useful for debugging the decision process in classification networks.
