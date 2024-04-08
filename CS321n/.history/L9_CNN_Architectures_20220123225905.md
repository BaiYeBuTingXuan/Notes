# CNN Architecture

## LIST

1. AlexNet
2. VGG
3. GoogleNet
4. ResNet
5. Others

## AlexNet
### Architecture
0. [227 * 227 * 3]INPUT
1. [55 * 55 * 96]CONV1:96 11 * 11 fliters at stride 4,pad 0
2. [27 * 27 * 96]MAX POOL 1:3 * 3 fliters at stride 3
3. [27 * 27 * 96]NORM1
4. [27 * 27 * 256]CONV2:256 5 * 5 fliters at stride 1,pad 2
5. [13 * 13 * 256]MAX POOL 2:3 * 3 fliters at stride 2
6. [13 * 13 * 256]NORM2
7. [13 * 13 * 384]CONV3:384 3 * 3 fliters at stride 1,pad 1
8. [13 * 13 * 384]CONV4:384 3 * 3 fliters at stride 1,pad 1
9. [13 * 13 * 256]CONV5:256 3 * 3 fliters at stride 1,pad 1
10. [6 * 6 *256]MAX POOL 3:3 * 3 fliters at stride 2
11. [4096]FC1:4096 neurons
12. [4096]FC2:4096 neurons
13. [1000]FC3:1000 neurons

### ZFNet
AlexNet but：
CONV1 :from 11 * 11 stride 4 to 7 * 7 stride 2
CONV3,4,5 :from 384,384,256 filters use 512,1024,512


## VGG
## GoogleNet
## ResNet
## Others