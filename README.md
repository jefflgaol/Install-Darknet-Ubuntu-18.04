# Install-Darknet-Ubuntu-18.04
## Step 1: Clone Darknet
```
$ cd ~
$ git clone https://github.com/pjreddie/darknet
$ cd darknet
```
## Step 2: Change checkpoints saving period
```
$ gedit ~/darknet/examples/detector.c
```
Originally, darknet will save every 100 iterations until first 1000. Then, it saves every 10000 iterations. You can modify it according to your needs. If you want to save every 100 iterations until the first 1000, then save every 4000 iterations, then you can replace this:
```
if(i%10000==0 || (i < 1000 && i%100 == 0)){
```
with this one
```
if(i%4000==0 || (i < 1000 && i%100 == 0)){
```
## Step 3: Modify Makefile
```
$ gedit ~/darknet/Makefile
```
Make sure you have this configuration:
```
GPU=1
CUDNN=1
OPENCV=1
OPENMP=0
DEBUG=0
ARCH= -gencode arch=compute_61,code=compute_61
```
## Step 4: Install OpenCV library
```
$ sudo apt-get install libopencv-dev 
```
## Step 5: Change gcc
https://github.com/ethereum-mining/ethminer/issues/731#issuecomment-395195527
```
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 10
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 10
```
## Step 6: Make
```
$ make -j $(($(nproc) + 1))
```
