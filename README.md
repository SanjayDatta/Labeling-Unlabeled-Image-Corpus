# Labeling-Unlabeled-Image-Corpus
## Abstract: Efficient Labeling of Unlabeled images 
### **Overall ~87% accuracy was achieved on an unlabeled image corpus (10440) at 5% manual labeling effort**
The balance 13% error images can be corrected 1 by 1 in a targeted manner to take labeling accuracy to 100%. A work flow has been provided to do it correctly and efficiently. 
### **So with 18% (~5 + ~13) effort, an image corpus can be labeled 100% accurately.**

## Efficient Labeling of Unlabeled images
1. Take a large corpus of unlabeled images.
2. Represent each image as a 1001-dimensional vector using ImageNet pre-trained model.
3. Cluster images using PsyFing™, a multi-level clustering algorithm. It brings together the most distinctive images of the corpus and assign the most similar of them respectively to form a number of cluster centers. Then balance images get allocated to the cluster with which it has the highest similarity (novel Bonding Quotient™).
4. A level k cluster center contains $2^k$ images. These images almost always are of the same brand, particularly at the lower level clustering. At higher level, it sometimes gets mixed up with similar looking but different brands in the same cluster center.
5. We will use this property to manually label images in cluster centers at $2^k$ efficiency to build adequate size training data for classification. Number of clusters for 10440 images corpora at levels 1 to 6 were: 2513-594-144-36-6-1. An example of each level shown below:
6. 2513 is too many to label. Level 2 is just right with only 9 out of 594 clusters contain mixed up brands. We get 2340 (~22%) labeled images by looking at only 585 level 2 cluster centers. Randomly chosen 22% for training is low. But here, they have properties of cluster center. This boosts efficiency of classification.
![Image description](https://github.com/SanjayDatta/Labeling-Unlabeled-Image-Corpus/blob/master/cluster_center_levelwise.jpg)
