# YOLOv1 with Tensorflow 2

Paper :- [You Only Look Once:
Unified, Real-Time Object Detection](https://arxiv.org/pdf/1506.02640.pdf)

[DagsHub Repository](https://dagshub.com/Bharat-mtr/yolov1-tf2)



![tf-v2.5.0](https://img.shields.io/badge/TensorFlow-v2.5.0-orange)

For ease of implementation, i have not implemented exactly the same as paper.  
The things presented below are implemented differently from the paper.

- Backbone network. (Used **Xception** instead of network mentioned in the paper.)

- Learning rate schedule (Used `tf.keras.optimizers.schedules.ExponentialDecay`)

- Data augmentations

- Hyper parameters

- And so on . . .

<br><br>

## Preview

### Tensorboard

<div align="center">
<a href="./preview/tb_scalars_val_aps.jpeg">
<img src="./preview/tb_scalars_val_aps.jpeg" width="400" height="240">
</a>
<a href="./preview/tb_scalars_lr_losses.jpeg">
<img src="./preview/tb_scalars_lr_losses.jpeg" width="400" height="240">
</a>
</div>

<div align="center">
<a href="./preview/tb_imgs_train.jpeg">
<img src="./preview/tb_imgs_train.jpeg" width="400" height="240">
</a>
<a href="./preview/tb_imgs_val.jpeg">
<img src="./preview/tb_imgs_val.jpeg" width="400" height="240">
</a>
</div>

<br>

### Inference Visualization

<div align="center">
<a href="./preview/voc2007_test_sample01_viz.jpeg">
<img src="./preview/voc2007_test_sample01_viz.jpeg" width="400" height="240">
</a>
<a href="./preview/voc2007_test_sample02_viz.jpeg">
<img src="./preview/voc2007_test_sample02_viz.jpeg" width="400" height="240">
</a>
</div>

<div align="center">
<a href="./preview/voc2007_test_sample03_viz.jpeg">
<img src="./preview/voc2007_test_sample03_viz.jpeg" width="400" height="240">
</a>
<a href="./preview/voc2007_test_sample04_viz.jpeg">
<img src="./preview/voc2007_test_sample04_viz.jpeg" width="400" height="240">
</a>
</div>

<br><br>

## Build Environment with Docker

### Build Docker Image

```bash
$ docker build -t ${NAME}:${TAG} .
```

### Create a Container

```bash
$ docker run -d -it --gpus all --shm-size=${PROPER_VALUE} ${NAME}:${TAG} /bin/bash
```

<br><br>

## Training Dataset: Pascal VOC Dataset ([VOC2008](https://dagshub.com/Bharat-mtr/yolov1-tf2/src/master/data/VOC2008) | [VOC2012](https://dagshub.com/Bharat-mtr/yolov1-tf2/src/master/data/VOC2012))

> Pascal VOC Dataset with [TFDS](https://www.tensorflow.org/datasets/overview)

### Number of Images

|                 | Train | Validation | Test                   |
|-----------------|-------|------------|------------------------|
| Pascal VOC 2008 | 2501  | 2510       | 4952 (Used Validation) |
| Pascal VOC 2012 | 5717  | 5823       | 10991 (No labels)      |

- Training Set: VOC2008 trainval + VOC2012 trainval (Total: 16551)
- Validation Set: VOC2008 test (Total: 4952)

<br><br>

## Pretrained PB File

Trained with default values of this repo. (Total Epoch: 105)

- **Download pb file: \<[Link](https://dagshub.com/Bharat-mtr/yolov1-tf2/src/master/model/yolo_voc_448x448.tar.gz)\>**

pb file is uploaded as `tar.gz`. So, you have to decompress this file like below.

```bash
$ tar -zxvf yolo_voc_448x448.tar.gz
```

If you want to inference with this pb file, infer to [inference_tutorial.ipynb](./inference_tutorial.ipynb)

<br>

### Performance

#### Evaluation with VOC2008 test

| class name  | AP         |
|-------------|------------|
| dog         | 0.7464     |
| pottedplant | 0.2250     |
| car         | 0.5021     |
| person      | 0.4482     |
| tvmonitor   | 0.5213     |
| diningtable | 0.4564     |
| bicycle     | 0.5927     |
| chair       | 0.2041     |
| motorbike   | 0.5595     |
| sofa        | 0.4801     |
| bus         | 0.6215     |
| boat        | 0.3274     |
| horse       | 0.7049     |
| aeroplane   | 0.5872     |
| sheep       | 0.4223     |
| bottle      | 0.1312     |
| train       | 0.7917     |
| cat         | 0.8044     |
| bird        | 0.4824     |
| cow         | 0.4548     |
| **mAP**     | **0.5032** |

<br>

#### Inference Speed

- GPU(GeForce RTX 3090): About 8 FPS
- CPU(AMD Ryzen 5 5600X 6-Core Processor): About 4 FPS

<br><br>

## Training Script

> Path: [./voc_scripts/train_voc.py](./voc_scripts/train_voc.py)

```bash
$ python train_voc.py
```

**Options**  

Default option values are [./configs/configs.py](./configs/configs.py).  
If the options are given, the default config values are overridden.  

- `--epochs`: Number of training epochs
- `--init_lr`: Initial learning rate
- `--lr_decay_rate`: Learning rate decay rate
- `--lr_decay_steps`: Learning rate decay steps
- `--batch_size`: Training batch size
- `--val_step`: Validation interval during training
- `--tb_img_max_outputs `: Number of visualized prediction images in tensorboard
- `--train_ds_sample_ratio`: Training dataset sampling ratio
- `--val_ds_sample_ratio`: Validation dataset sampling ratio

<br>

## Evaluation Script

> Path: [./voc_scripts/eval_voc.py](./voc_scripts/eval_voc.py)

Evaluation pretrained model with VOC2008 Test Dataset

```bash
$ python eval_voc.py
```

**Options**  

- `--batch_size`: Evaluation batch size (Default: batch_size of [./configs/configs.py](./configs/configs.py).)
- `--pb_dir`: Save pb directory path (Default: `./ckpts/voc_ckpts/yolo_voc_448x448`)

<br><br>

## Citation

**You Only Look Once: Unified, Real-Time Object Detection** \<[arxiv link](https://arxiv.org/abs/1506.02640)\>

```
@misc{redmon2016look,
      title={You Only Look Once: Unified, Real-Time Object Detection}, 
      author={Joseph Redmon and Santosh Divvala and Ross Girshick and Ali Farhadi},
      year={2016},
      eprint={1506.02640},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```
