
Exploration of DATA: 'How to deal with the Single or Few shots (59.4% of only shots)

Here are the solutions we discussed; Siamese Network, ArcFace, OSR(Open-set recognition)-openmax+

What we decided to focus? 'ArcFace'

The process I've chosen: 
  1) to preprocess using 'yolov5' to focus on the main feature, 'back fin'.
  2) some of the species had no relations with the feature, but they were very few. ex) belugas
  3) And followed one of the most featured code with ArcFace-ConvNext (70% of accuracy)




----------------------------------------
The summary of the 1st place solution;
  1) Tuning of dynamic margin hyperparameters with Optuna
  2) Larger learning rate for ArcFace head (10 times bigger than efficientnet_b7)
  3) Bounding box mixing augmentation 
    :For train data, they randomly mixed several bboxes with the certain ratio of fullbody/fullbody_charm/backfin/detic(labled boxes)/none.(60,15,15,5,5)
    Esp backfin images significantly impoved the performance (made the model robust), and also a few non-cropped images were used for regularization.
    Used augmentation a lot, and 'handling flipped images as different classes' largely enhanced the performance.
    
  4) Ensemble of knn and logit
  5) Two-round pseudo labeling
     :To deal with the highly imbalanced data & distribution and 'new_individual'(OSR part), they tried to label the data using KNN so that they could    guess the distribution of the open-set data, which was not in the training set. They added, 'additional rounds of pseudo labeling might have further improved performance.'

  6) Ensemble of many models
    : But the best performance in a single model was achieved by efficientnet_b7.
    And they concatenated those two GeM-pooled feature maps and passed them to ArcFace with dynamic margins TWICE.
    (1 for the hyperparameter tuning of the imbalced data (with Optuna), which is too sensitive to the parameters,
     1 for classifying species and it worked better than linear one.)




+) What they tried and not worked (Other options for CV):
  - input 4-channel images with segmentation mask (1st place solution of the last competition)
  - input 6-channel images combining 2 types of images cropped by fullbody and backfin bboxes
  - input rectangle images such as (512, 1024)
  - maintain aspect ratio of images by bounding box expansion instead of resizing
  - AdaCos, triplet loss (Siamese Network)
  - Focal loss
  - training p of GeM pooling
  - ConvNeXt
  - Swin Transformer (384 was too small)
  - dolg
  - using pseudo labels for knn
  - cutmix

https://www.kaggle.com/competitions/happy-whale-and-dolphin/discussion/320192
