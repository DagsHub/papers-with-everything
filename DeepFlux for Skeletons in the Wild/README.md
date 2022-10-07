# DeepFlux for Skeletons in the Wild

[The DagsHub Repo](https://dagshub.com/Bharat-mtr/DeepFlux)

Computing object skeletons in natural images is challenging, owing to large variations in object appearance and scale, and the complexity of handling background clutter. Many recent methods frame object skeleton detection as a binary pixel classification problem, which is similar in spirit to learning-based edge detection, as well as to semantic segmentation methods. In the present article, we depart from this strategy by training a CNN to predict a twodimensional vector field, which maps each scene point to a candidate skeleton pixel, in the spirit of flux-based skeletonization algorithms. This “image context flux” representation has two major advantages over previous approaches. First, it explicitly encodes the relative position of skeletal pixels to semantically meaningful entities, such as the image points in their spatial context, and hence also the implied object boundaries. Second, since the skeleton detection context is a region-based vector field, it is better able to cope with object parts of large width. We evaluate the proposed method on three benchmark datasets for skeleton detection and two for symmetry detection, achieving consistently superior performance over state-of-the-art methods.

The code and trained models of:

DeepFlux for Skeletons in the Wild, CVPR 2019 [[Paper]](http://openaccess.thecvf.com/content_CVPR_2019/papers/Wang_DeepFlux_for_Skeletons_in_the_Wild_CVPR_2019_paper.pdf)

## Prerequisite

- Caffe and VGG-16 pretrained model [[VGG_ILSVRC_16_layers.caffemodel]](http://www.robots.ox.ac.uk/~vgg/software/very_deep/caffe/VGG_ILSVRC_16_layers.caffemodel)

- Datasets: [[SK-LARGE]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/data/SK-LARGE), [[SYM-PASCAL]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/data/SymPASCAL-by-KZ)

- OpenCV 3.4.3 (C++ or Python, optional)

- MATLAB

## Usage

#### 1. Install Caffe

```bash

cp Makefile.config.example Makefile.config
# adjust Makefile.config (for example, enable python layer)
make all -j16
# make sure to include $CAFFE_ROOT/python to your PYTHONPATH.
make pycaffe

```

Please refer to [Caffe Installation](http://caffe.berkeleyvision.org/install_apt.html) to ensure other dependencies.

#### 2. Data and model preparation

```bash

# download datasets and pretrained model then
mkdir data && mv [your_dataset_folder] data/
mkdir models && mv [your_pretrained_model] models/
# data augmentation
cd data/[your_dataset_folder]
matlab -nodisplay -r "run augmentation.m; exit"

```

#### 3. Training scripts

```bash

# an example on SK-LARGE dataset
cd examples/DeepFlux/
python train.py --gpu [your_gpu_id] --dataset sklarge --initmodel ../../models/VGG_ILSVRC_16_layers.caffemodel

```

For training an end-to-end version of DeepFlux, adding the `--e2e` option.

#### 4. Evaluation scripts

```bash

# an example on SK-LARGE dataset
cd evaluation/
# inference with C++
./eval_cpp.sh ../../data/SK-LARGE/images/test ../../data/SK-LARGE/groundTruth/test ../../models/sklarge_iter_40000.caffemodel
# inference with Python
./eval_py.sh ../../data/SK-LARGE/images/test ../../data/SK-LARGE/groundTruth/test ../../models/sklarge_iter_40000.caffemodel
# inference with Python (end-to-end version)
./eval_py_e2e.sh ../../data/SK-LARGE/images/test ../../data/SK-LARGE/groundTruth/test ../../models/sklarge_iter_40000.caffemodel

```

## Results and Trained Models

#### SK-LARGE

| Backbone | F-measure | Comment & Link |
|:-------------:|:-------------:|:-----:|
| VGG-16 | 0.732 | CVPR submission [[Model]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/model/sklarge_iter_40000_CVPR.caffemodel) |
| VGG-16 | 0.735 | different_lr [[Model]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/model/sklarge_iter_40000_DifferentLR.caffemodel) |
| VGG-16 | 0.737 | end-to-end [[Model]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/model/0.737_sklarge_iter_40000_end2end.caffemodel) |
<!-- | ResNet-101 | 0.752 | different_lr [[Available soon]]() | -->

#### SYM-PASCAL

| Backbone | F-measure | Comment & Link |
|:-------------:|:-------------:|:-----:|
| VGG-16 | 0.502 | CVPR submission [[Model]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/model/sympascal_iter_40000_CVPR.caffemodel) |
| VGG-16 | 0.558 | different_lr [[Model]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/model/sympascal_iter_40000_DifferentLR.caffemodel) |
| VGG-16 | 0.569 | end-to-end [[Model]](https://dagshub.com/Bharat-mtr/DeepFlux/src/master/model/0.569_sympascal_iter_40000.caffemodel) |
<!-- | ResNet-101 | 0.584 | different_lr [[Available soon]]() | -->

>*different_lr means different learning rates for backbone and additional layers

>*lambda=0.4, k1=3, k2=4 for all models with post-processing
