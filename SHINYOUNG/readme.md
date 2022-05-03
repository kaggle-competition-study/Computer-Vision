
Exploration of DATA: 'How to deal with the Single or Few shots (59.4% of only shots)
Here are the solutions we discussed; Siamese Network, ArcFace, OSR(Open-set recognition)-openmax+
What we decided to focus? 'ArcFace'
The process I've chosen: 
  1) to preprocess using 'yolov5' to focus on the main feature, 'back fin'.
  2) some of the species had no relations with the feature, but they were very few. ex) belugas
  3) And follow one of the most featured code with ArcFace-ConvNext (70% of accuracy)
