# RotationNet

RotationNet takes multi-view images of an object as input and jointly estimates its pose and object category.  
We got **the first prize** at Task 1 in [the SHREC2017 Large-scale 3D Shape Retrieval from ShapeNet Core55 Challenge](https://shapenet.cs.stanford.edu/shrec17/#results) and got **the first prize** at [the SHREC2017 RGB-D Object-to-CAD Retrieval Contest](http://people.sutd.edu.sg/~saikit/projects/sceneNN/shrec17/evaluation/)!  
Please see [SHREC2017\_track3 repository](https://github.com/kanezaki/SHREC2017_track3) to reproduce our results on SHREC2017 track3.  

![RotationNet](https://staff.aist.go.jp/kanezaki.asako/images/RotationNet2.jpg "Inference Process")

Asako Kanezaki, Yasuyuki Matsushita and Yoshifumi Nishida.
**RotationNet: Joint Object Categorization and Pose Estimation Using Multiviews from Unsupervised Viewpoints.** 
*arXiv preprint arXiv:1603.06208*, 2017.
([pdf](https://arxiv.org/abs/1603.06208))


## Requirement

### 1. Prepare [caffe-rotationnet2](https://github.com/kanezaki/caffe-rotationnet2)
    $ git clone https://github.com/kanezaki/caffe-rotationnet2.git  
    $ cd caffe-rotationnet2  
  
Prepare your Makefile.config and compile.  

    $ make; make pycaffe

### 2. Download scripts
    $ git clone https://github.com/kanezaki/rotationnet.git  
    $ cd rotationnet

### 3. Download pre-trained models
    $ wget https://staff.aist.go.jp/kanezaki.asako/pretrained_models/rotationnet_modelnet40_case1.caffemodel  
    $ wget https://staff.aist.go.jp/kanezaki.asako/pretrained_models/rotationnet_modelnet40_case2.caffemodel

## Getting started
   Change 'caffe\_root' in save_scores.py to your path to caffe-rotationnet2 repository.  
   Run the demo script.  

    $ bash demo.sh

## Reproduce results on ModelNet40

### 1. Download multi-view images generated in [Su et al. 2015]
    $ bash get_modelnet_png.sh  
    [Su et al. 2015] H. Su, S. Maji, E. Kalogerakis, E. Learned-Miller. Multi-view Convolutional Neural Networks for 3D Shape Recognition. ICCV2015.  
   
### 2. Save scores and do predictions
    $ bash test_modelnet40.sh  

## Train your own RotationNet models

### 1. Download multi-view images generated in [Su et al. 2015]
    $ bash get_modelnet_png.sh  

### 2. Download initial weights for fine-tuning the models
   Please download the file "ilsvrc_2012_train_iter_310k" according to [R-CNN repository](https://github.com/rbgirshick/rcnn)  
   This is done by the following command:  

    $ wget http://www.cs.berkeley.edu/~rbg/r-cnn-release1-data.tgz  
    $ tar zxvf r-cnn-release1-data.tgz  

### 3. Run the training operation
#### 3-1. Case (2): Train the model w/o upright orientation (RECOMMENDED)
    $ ./caffe-rotationnet2/build/tools/finetune_net.bin Training/rotationnet_modelnet40_case2_solver.prototxt caffe_nets/ilsvrc_2012_train_iter_310k 2>&1 | tee log.txt  
#### 3-2. Case (1): Train the model with upright orientation
    $ ./caffe-rotationnet2/build/tools/finetune_net.bin Training/rotationnet_modelnet40_case1_solver.prototxt caffe_nets/ilsvrc_2012_train_iter_310k 2>&1 | tee log.txt  


## Reproduce results on SHREC2017 track3 (Large-scale 3D Shape Retrieval from ShapeNet Core55)
   Please see [SHREC2017\_track3 repository](https://github.com/kanezaki/SHREC2017_track3)
