# CNN Architecture

## LIST

1. AlexNet
2. VGG
3. GoogleNet
4. ResNet
5. Others

## AlexNet
### Architecture
5+3 layers of CONV+POOL,2 NORM and 3 FC
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
```
Smaller filters,Deeper networks
```

VGG16 as below:
![avatar](./L9_Pic1.png)

8 layers AlexNet --> 16-19 layers

Only 3 * 3 CONV stride 1,pad 1 and 2*2 MAX POOL stride 2

Q1:Why smaller filters?
Ans:Stack of three 3*3 conv（stride）layers has same __effective__ __receptive__ __field__ (有效感知域)as one 7 * 7 layers but fewer parameters.

Q2:What is the __effective__ __receptive__ __field__ of three 3 * 3 conv(stride 1) layers
Ans:7 * 7;3 * 3 ---> 5 * 5 ---> 7 * 7.

## GoogleNet

```
Deeper networks,with computational efficiency
```
## ResNet
## Others