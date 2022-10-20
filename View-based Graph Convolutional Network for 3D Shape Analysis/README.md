# Pytorch code for view-GCN [CVPR2020].

Xin Wei, Ruixuan Yu and Jian Sun. **View-GCN: View-based Graph Convolutional Network for 3D Shape Analysis**. CVPR, accepted, 2020. [[pdf]](http://openaccess.thecvf.com/content_CVPR_2020/papers/Wei_View-GCN_View-Based_Graph_Convolutional_Network_for_3D_Shape_Analysis_CVPR_2020_paper.pdf) [[supp]](http://openaccess.thecvf.com/content_CVPR_2020/supplemental/Wei_View-GCN_View-Based_Graph_CVPR_2020_supplemental.pdf)

[DAGsHub Repository](https://dagshub.com/Bharat-mtr/view-GCN)

## Citation
If you find our work useful in your research, please consider citing:
```
@InProceedings{Wei_2020_CVPR,
author = {Wei, Xin and Yu, Ruixuan and Sun, Jian},
title = {View-GCN: View-Based Graph Convolutional Network for 3D Shape Analysis},
booktitle = {IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2020}
}
```

## Training

### Requiement

This code is tested on Python 3.6 and Pytorch 1.0 + 

### Dataset

First download the 20 views ModelNet40 dataset provided by [[DAGsHub Download link]](https://dagshub.com/Bharat-mtr/view-GCN/src/master/data) and put it under `data`



### Command for training:

`python train.py -name view-gcn -num_models 0 -weight_decay 0.001 -num_views 20 -cnn_name resnet18`

The code is heavily borrowed from [[mvcnn-new]](https://github.com/jongchyisu/mvcnn_pytorch).

We also provide a [trained view-GCN network](https://dagshub.com/Bharat-mtr/view-GCN/src/master/model_weight) achieving 97.6% accuracy on ModelNet40.

## Reference
Asako Kanezaki, Yasuyuki Matsushita and Yoshifumi Nishida. RotationNet: Joint Object Categorization and Pose Estimation Using Multiviews from Unsupervised Viewpoints. CVPR, 2018.

Jong-Chyi Su, Matheus Gadelha, Rui Wang, and Subhransu Maji. A Deeper Look at 3D Shape Classifiers. Second Workshop on 3D Reconstruction Meets Semantics, ECCV, 2018.

