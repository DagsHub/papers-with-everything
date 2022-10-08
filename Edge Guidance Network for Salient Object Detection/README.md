# EGNet
EGNet: [Edge Guidance Network for Salient Object Detection (ICCV 2019)](https://openaccess.thecvf.com/content_ICCV_2019/papers/Zhao_EGNet_Edge_Guidance_Network_for_Salient_Object_Detection_ICCV_2019_paper.pdf)


[DagsHub Repository](https://dagshub.com/Bharat-mtr/EGNet)


We use the sal2edge.m to generate the edge label for training.
### For training:
1. Clone this code by `git clone https://github.com/bharat-mtr/EGNet.git --recursive`, assume your source code directory is`$EGNet`;

2. Download [training data](https://dagshub.com/Bharat-mtr/EGNet/src/master/data);

3. Download [initial model](https://dagshub.com/Bharat-mtr/EGNet/src/master/models/initial_model); 

4. Change the image path and intial model path in run.py and dataset.py;

5. Start to train with `python3 run.py --mode train`.

### For testing:
1. Download [pretrained model](https://dagshub.com/Bharat-mtr/EGNet/src/master/models/model); 

2. Change the test image path in dataset.py 

3. Generate saliency maps for SOD dataset by `python3 run.py --mode test --sal_mode s`, PASCALS by `python3 run.py --mode test --sal_mode p` and so on;

4. Testing code we use is the public open source code. (https://github.com/Andrew-Qibin/SalMetric)



### Pretrained models, datasets and results:
| [Page](https://mmcheng.net/jxzhao/) |
| [Training Set](https://dagshub.com/Bharat-mtr/EGNet/src/master/data) |
| [Pretrained models](https://dagshub.com/Bharat-mtr/EGNet/src/master/models/model) (2cf5) |
| [VGG](https://dagshub.com/Bharat-mtr/EGNet/src/master/models/Result_VGG) [resnet](https://dagshub.com/Bharat-mtr/EGNet/src/master/models/Result_ResNet50)|


### If you think this work is helpful, please cite
```latex
@inproceedings{zhao2019EGNet,
 title={EGNet:Edge Guidance Network for Salient Object Detection},
 author={Zhao, Jia-Xing and Liu, Jiang-Jiang and Fan, Deng-Ping and Cao, Yang and Yang, Jufeng and Cheng, Ming-Ming},
 booktitle={The IEEE International Conference on Computer Vision (ICCV)},
 month={Oct},
 year={2019},
}
```

### Other related work
Contrast Prior and Fluid Pyramid Integration for RGBD Salient Object Detection. (CVPR2019) [page](https://mmcheng.net/rgbdsalpyr/)



