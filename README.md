# Amodal Instance Segmentation with Transformer
Table of Contents
* [Introduction](#introduction)
* [Usage](#usage)
* [Trained models](#trained-models)
* [Acknowledgement](#acknowledgement)
* [Citation](#citation)

## Introduction
![alt text](assets/arch.png "AISFormer architecture")

The figure above illustrates our AISFormer architecture. The main implementation of this network can be foundd [here](detectron2/modeling/roi_heads/aisformer/aisformer.py).

## Usage
### 1. Installation
```
conda create -n aisformer python=3.8 -y
source activate aisformer 

conda install pytorch==1.10.0 torchvision==0.11.0 cudatoolkit=11.3 -c pytorch
pip install ninja yacs cython matplotlib tqdm
pip install opencv-python==4.4.0.40
pip install scikit-image
pip install timm==0.4.12

# coco api
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
python setup.py build_ext install


git clone https://github.com/UARK-AICV/AISFormer
cd AISFormer/
python3 setup.py build develop
# optional, just in case
pip install setuptools==59.5.0
pip install torch-dct
```
### 2. Data preparation
#### KINS dataset
Download the [Images](http://www.cvlibs.net/download.php?file=data_object_image_2.zip)
from [KITTI dataset](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=2d). 

The [Amodal Annotations](https://drive.google.com/drive/folders/1FuXz1Rrv5rrGG4n7KcQHVWKvSyr3Tkyo?usp=sharing)
could be found at [KINS dataset](https://github.com/qqlu/Amodal-Instance-Segmentation-through-KINS-Dataset)

#### D2SA dataset
The D2S Amodal dataset could be found at [mvtec-d2sa](https://www.mvtec.com/company/research/datasets/mvtec-d2s/).

#### COCOA-cls dataset
The COCOA dataset annotation from [here](https://drive.google.com/file/d/1n1vvOaT701dAttxxGeMKQa7k9OD_Ds51/view) (reference from github.com/YihongSun/Bayesian-Amodal)
The images of COCOA dataset is the train2014 and val2014 of [COCO dataset](http://cocodataset.org/).

#### Expected folder structure for each dataset
AISFormer support datasets as coco format. It can be as follow (not necessarily the same as it depends on register data code)
```
KINS/
|--train_imgs
|--test_imgs/
|--annotations/
|----train.json
|----test.json
```
Then, See [here](detectron2/data/datasets/builtin.py) for more details on data registration

After registering, run the preprocessing scripts to generate occluder mask annotation, for example:
```
python -m detectron2.data.datasets.process_data_amodal \
   /path/to/KINS/train.json \
   /path/to/KINS/train_imgs \
   kins_dataset_train
```
the expected new annotation can be as follow:
```
KINS/
|--train_imgs
|--test_imgs/
|--annotations/
|----train.json
|----train_amodal.json
|----test.json
```

### 3. Training, Testing and Demo
Configuration files for training AISFormer on each datasets are available [here](configs/).
To train, test and run demo, see the example scripts at [`scripts/`](scripts/):

## Trained models
Available soon!

## Acknowledgement
This code utilize [BCNet](https://github.com/lkeab/BCNet) for dataset mapping with occluder, [VRSP-Net](https://github.com/YutingXiao/Amodal-Segmentation-Based-on-Visible-Region-Segmentation-and-Shape-Prior) for amodal evalutation, and [detectron2](https://github.com/facebookresearch/detectron2) as entire pipeline with Faster RCNN meta arch.

## Citation
Available soon!
