# Class-Activation-Map

## MOTIVATION:
This technique allows re-using classifiers for getting good localization results even when training without bounding box coordinates data

You don't need to draw a box, simply train a classifier - you can automatically know where the object is.

![0000001](https://user-images.githubusercontent.com/51057490/82156080-058bdd00-9871-11ea-9ee2-0a07df56c055.JPG)



*Class activation maps* are a simple technique to get the discriminative image regions used by a CNN to identify a specific class in the image. 
In other words, a class activation map (CAM) lets us see which regions in the image were relevant to this class  
The corresponding weights of the feature vector connected to the logistic regression aids to weight the importance of each object in the image in relation to a classification of a particular image. 

*In this kernel*, I used this workflow to get my Class Activation Map:

- *Load a Resnet50* pretrained on [Imagenet](http://www.image-net.org/) but cut it off at the last activation layer, which returns 2048 7x7 feature maps of the query image 

- *Use the Resnet50* model to predict the class of the query image

- *With the class of the query image*, take the corresponding weights of the logistic regression, i.e the last dense layer weights

- *Compute the dot product* of the 2048 7x7 feature maps and the logistic regression weights of the query image class, returns 7x7 image

- *Upsample the 7x7 image* to the original size of the image using [scipy](https://www.scipy.org/)

- *Overlay a sort of heatmap* over the query image

- *Plot* both the query image and its overlayed heatmap constituent  

![0000002](https://user-images.githubusercontent.com/51057490/82155893-e9d40700-986f-11ea-9b8a-b68e96cc566f.JPG)
![0000004](https://user-images.githubusercontent.com/51057490/82155996-8c8c8580-9870-11ea-98e5-cb019af3ed67.JPG)
![0000000088](https://user-images.githubusercontent.com/51057490/82156029-c2316e80-9870-11ea-89f6-f88153ac3a12.JPG)
![0000003](https://user-images.githubusercontent.com/51057490/82156047-e4c38780-9870-11ea-8329-0967f07c88e1.JPG)
![0000007](https://user-images.githubusercontent.com/51057490/82156068-015fbf80-9871-11ea-94c9-eeb4f6a87150.JPG)
![0000006](https://user-images.githubusercontent.com/51057490/82156085-091f6400-9871-11ea-9eea-a313a4a78c22.JPG)
![0000005](https://user-images.githubusercontent.com/51057490/82156093-0d4b8180-9871-11ea-99f4-9aad2f64f8a3.JPG)
![000000010](https://user-images.githubusercontent.com/51057490/82156095-11779f00-9871-11ea-84f5-c2d86d2a74f7.JPG)
![0000009](https://user-images.githubusercontent.com/51057490/82156102-189ead00-9871-11ea-90f6-339b25369f36.JPG)
![0000008](https://user-images.githubusercontent.com/51057490/82156115-28b68c80-9871-11ea-8089-41c26e6f7719.JPG)
![bicycle](https://user-images.githubusercontent.com/51057490/82156123-30763100-9871-11ea-94d1-d1e72442e896.JPG)

N/B: The area around the main object which the network presumes is relevant for it's prediction is hotter than the rest, hence the name, "heatmap"


## CONCLUSION:
- This also shows how deep learning networks already have some kind of a built in attention mechanism.

- This should be useful for debugging the decision process in classification networks.
