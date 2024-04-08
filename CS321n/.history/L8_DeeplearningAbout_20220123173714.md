# DeepLearning About

## LIST

1. CPUs and GPUs
2. Hyperparameters
3. Image


## CPUs and GPUs

- CPU ： Central Processing Unit
  - Fewer cores but each cores is much faster and much more capable
  - Great at squential  tasks
- GPU :  Graphics Processing Unit
  - More cores,but each core is much slower and "dumber"
  - Great for parallel tasks,like mutipulation of matrix

![avatar](./L8_Pic1.png)

In deeplearning,we usaully use NVIDIA rather than AMD.

### Programming on GPUs
- CUDA(NVIDIA only)
  - Write C-like code that run directly on GPU
  - Higher level APIs:cuBLAS,cuFFT,cuDNN,etc
- OpenCL
  - Similer to CUDA,but runs on anything
  - Usually slower

### Disk
The model is stored in GPUs but the large data are stored in the disk.If uncarefully,the trainning can bottleneck on reading data and transfering to GPU.

Solution:
- Read all data into RAM
- Use SSD instead of HDD
- Use mutiple CPU threads to perfetch data.

## DeepLearning Framework

- Caffe 
- Torch --> Pytorch
- Theano --> TensorFlow

### Torch

### TensorFlow

### Caffe