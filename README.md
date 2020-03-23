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
7. Using Nearest Neighbor Classification, achieved test data accuracy of ~84%. So overall accuracy based on this approach was ~87% (84% x 75-80% + 100% x 20-25%).
8. Depending on time available, these specific 13% error images can also be manually labeled leading to 100% accuracy.
9. So, 100% accuracy can be obtained by manually labeling effort of only 18% (5+13) of the corpus.
## More concretely:
1. **Dataset: 13184 product shots detected from grocery store shelf images** [grocerydataset](https://github.com/gulvarol/grocerydataset). Only 2744 labeled images have been used for classifier learning. The balance 10440 unlabelled images from class 0 could not be used. 
2. **Objective: to efficiently label unlabeled data using clustering.** Here clustering will be used to identify the `most similar and distinctive` of images from the dataset and label them manually to build training dataset. 
3. **Feature vector:** Use predictor of [tensorflow_hub classifier](https://www.tensorflow.org/tutorials/images/transfer_learning_with_hub) and generate 1001-dimensional vector to represent each image
4. **Feature transformation:** Transform raw feature vector thru a series of 5 stages of feature transformation. It is scaled and weighted using properties of specific distribution of data among others
5. **Similarity metric:** Transformation gives a measure of similarity between images (a novel measure, Bonding Quotient)
6. **Clustering:** Ensures most similar groups of images come together as dense cluster centers and less similar gravitate to their respective closest cluster centers. These cluster centers represent the most similar, the most distinctive images from the dataset and also conveniently much fewer in number (PsyFing Clustering algorithm)
7. **Manually label these cluster center images** where size of task is of the order ~1/20 of all unlabeled data
8. Use **new labeled training data** as training and balance images as test data with unknown labels. Nearest neighbors of each test image will be found from new labeled training base
9. Label will be that of the **nearest neighbor**.
10. **Random check** for accuracy and updation of imcorrect label
11. **Efficient manual error correction work flow** provided in the end to improve accuracy of the labeling further.
