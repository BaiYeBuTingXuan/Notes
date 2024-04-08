# Classifying And Location

## List

## Double loss
To regconize the objects and locate it or draw the bounding-box,the neutral network produce two loss:one for regconization and another for location.The muti-task loss of the network is the combination of the two.

## R-CNN
Due to the complication of location of a object(thousands of tests),we can use ROI (Region of Interest)method,that chooses thousands of region,than do the classification.
![avatar](./L11_Pic1.png)

problem:
- Slow
- memory-consume

Solution:Fast R-CNN

## Fast R-CNN
![avatar](./L11_Pic2.png)
The Fast R-CNN costs most of time on computing the thousands of ROI.
![avatar](./L11_Pic3.png)
Solution:Faster R-CNN

## Faster R-CNN
Make CNN do proposals!
Insert Reigon Proposal Network(__RPN__)


