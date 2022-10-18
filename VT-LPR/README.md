# Vehicle and License Plate Recognition with Novel Dataset for Toll Collection

### <a href="https://dagshub.com/arnavr.neo/VT-LPR">The DagsHub Repo</a>

This repository is the implementation of Vehicle and License Plate Recognition with Novel Dataset for Toll Collection (VT-LPR). 


## Introduction
Tolling efficiency in manual toll collection system is low and time consuming, which results in delayed traffic and long queue of vehicles. This also requires human effort and resources. 

<p align="center">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/rush_2.png" width="300" title="hover text">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/rush_1.png" width="300" title="hover text">
</p>
Toll collection process is automated in some countries by installing sensors and Radio Frequency Identification (RFID) based system, but this comes with an additional cost of installing such systems. Utilizing the already installed cameras for survillence purposes, we automate the toll collection process by recognizing vehicle type and license plate from the image taken by the cameras.
We gather a Novel Vehicle type and License Plate Recognition Dataset called _Diverse Vehicle and License Plates Dataset (DVLPD)_ consisting of 10k images. We present an automated toll collection process which consists of three steps: Vehicle Type Recognition, License Plate Detection and Character Recognition. We train different state-of-the-art object detection models such as YOLO V2, YOLO V3, YOLO V4 and Faster RCNN. For the real-time application, we deploy our models on Raspberry Pi.


<br/><br/>
Vehicle and License Plate Recognition with Novel Dataset for Toll Collection [ [Paper link]. ](https://arxiv.org/abs/2202.05631)

## Requirements
* Python>=3.6
* Streamlit==1.0.0
* PyQt5==5.15.4
* PyQt5Designer==5.14.1
* OpenCV==4.5.1.48
* pillow
* matplotlib
* pandas
* numpy
* tensorflow
* tflite

Note: These packages can be installed through Pip package installer. This code is tested with these versions.

## Challenges
Image based vehicle type and license plate recognition include many challenges such as:
* Intra-class variations
* Background clutter
* Non-uniform position
* Multiple license plates
* Non-uniform fonts
* Partial occlusion
* Damaged license plates
* Lack of license plates

<p align="center">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/problems.jpg" title="hover text">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/variations.jpg" title="hover text">
</p>

## Methodology
### Dataset
We divide the Vehicle type and license plate recognition task into three steps: Vehicle type recognition, License plate localization and License plate character recognition. So we prepared three dataset named: _preprocessed dataset for Vehicle type recognition, lp-detect dataset for license plate location and lp-read dataset for license plate character recognition._
As we're training separate model for each task, all the vehicle images are annotated accordingly as shown below.

<img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/label.jpg" title="hover text">

### Framework

The proposed framework is aim to automatically collect toll amount by end-to-end image-based vehicle type and license plate recognition. Input to the model is an image and the outputs are recognized vehicle type and license plate character. When an image is fed to the first network called VT-Net, it recognize the vehicle type and crop the detection results. The cropped image is then fed to the secong network called LP-Net, which localize and crop the license plate. Finally, the last model called CR-Net is applied on the cropped license plate image to recognize the characters in the license plate.

<p align="center">
<img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/flow.jpg" width ="400" title="hover text">
<img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/chart.jpg" width ="450" title="hover text">
</p>

### Results
<p align="center">
<img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/type_res.jpg" width ="400" title="hover text">
<img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/lp_res.jpg" width ="320" title="hover text">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/Figs/lpr_res.jpg" width ="450" title="hover text">
</p>

## Test

1. Download the model weights from <a href='https://dagshub.com/arnavr.neo/VT-LPR'>here</a> by ruuning `dvc pull -r origin`.

2. Clone this repository

``` #2x
!git clone https://github.com/arnavrneo/VT-LPR.git
```

3. Put model weights in the downloaded folder.
4. Run the Streamlit code file using:

``` #2x
streamlit run streamlit_code.py
```
5. Run PyQt5 GUI using this command.


``` #2x
python vt_lpr_gui.py
```

## Single Image
<p align="center">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/results/Truck_0003.jpg" width="270" title="hover text">
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/results/S_0001.jpg" width="150" title="hover text">
<!--   <img src="results/single2.jpg" width="250" title="hover text"> -->
  <img src="https://github.com/arnavrneo/VT-LPR/blob/main/results/S_0002.jpg" width="220" title="hover text">
</p>
