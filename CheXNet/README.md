# CheXNet

[The DagsHub Repo](https://dagshub.com/nirbarazida/CheXNet)

### A Python3 (TensorFlow) reimplementation of CheXNet paper - Classification and Localization of Thoracic Diseases

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1U3F5ETJeisBnlmamR4EqigS7shIbL2L1)
## Prerequisites
- Python 3.8+
- TensorFlow 2.5+
- All the specified requirements in the text file

## Usage
1. Clone this repository.
2. Install requirements.txt using `pip install -r requirements.txt`.
3. Use DVC to pull the files that are stored on the DAGsHub remote storage by running `dvc pull`
4. Modify the code as you wish.
5. Run `dvc repro` to run the pipeline and train the model.

The resultant heatmaps from the evaluation stages should look something like 👇

![target-image](https://imgur.com/8bRDA9G.png)

## The ChestX-ray14 Dataset

[comment]: <> (Uncomment when streamlit is merged into master    ![]&#40;task_5_streamlit/images/Example.png&#41;)

The 45GB dataset comprises 112,120 frontal-view chest X-ray images organized 14 different folders, based on individual tarballs. There is a master list of images with target labels, image IDs, patient IDs alongside additional patient metadata.
[The dataset](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia) is available on the Kaggle platform.

### 1GB-Dataset
To use a smaller, subsampled dataset, run the following commands from the repository's root directory:
```bash
git update-index --assume-unchanged data_labeling/data.dvc
curl https://dagshub.com/nirbarazida/CheXNet/raw/d74cccbd0957c41dac7560565d2b7b4df3c0d195/data_labeling/data.dvc -o data_labeling/data.dvc
```

### Acknowledgements
- [Data](https://data.mendeley.com/datasets/rscbjbr9sj/2)
- License: CC BY 4.0
- [Citation](http://www.cell.com/cell/fulltext/S0092-8674(18)30154-5)

**Note:** *If you are adding/removing/moving files to different directories, it can affect the DVC pipeline, and therefore
the `dvc repro` command might not run properly.*