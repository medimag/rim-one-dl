# RIM-ONE DL

## RIM-ONE for Deep Learning

RIM-ONE DL is a unified retinal image database for assessing glaucoma using Deep Learning. **The full paper is available 
in this publication of the Image Analysis and Stereology journal**: https://www.ias-iss.org/ojs/IAS/article/view/2346

This repository hosts the RIM-ONE DL image dataset and the related data and tools, which consists of:

- The images divided into training and test sets. 
- The reference segmentations of the optic disc and cup for each image
- The tools to convert a reference segmentation to a NumPy array or to PNG
- The weights of the CNNs used in the publication

## Using the database

Data included in this database can only be used for research and educational purposes, free of charge and without
requesting permission to the authors. Copy, redistribution, and any unauthorized commercial use are prohibited.

In order to use this database and have comparable results among different publications, please use the original 
partitions described below for training and testing purposes. Moreover, **use only the data included in RIM-ONE DL**, do not 
add more images from different databases to train your model or tune your algorithm. 

**If you use RIM-ONE DL in your work, please cite the following publication:**

FUMERO BATISTA, Francisco José et al. RIM-ONE DL: A Unified Retinal Image Database for Assessing Glaucoma Using Deep 
Learning. Image Analysis & Stereology, v. 39, n. 3, p. 161-167, nov. 2020. ISSN 1854-5165. Available at: 
<https://www.ias-iss.org/ojs/IAS/article/view/2346>. doi: https://doi.org/10.5566/ias.2346.


BibTeX format:
```text
@article{RIMONEDLImageAnalStereol2346,
	author = {Francisco José Fumero Batista and Tinguaro Diaz-Aleman and Jose Sigut and Silvia Alayon and Rafael Arnay and Denisse Angel-Pereira},
	title = {RIM-ONE DL: A Unified Retinal Image Database for Assessing Glaucoma Using Deep Learning},
	journal = {Image Analysis & Stereology},
	volume = {39},
	number = {3},
	year = {2020},
	keywords = {Convolutional Neural Networks; Deep Learning; Glaucoma Assessment; RIM-ONE},
	issn = {1854-5165},
	pages = {161--167},
	doi = {10.5566/ias.2346},
	url = {https://www.ias-iss.org/ojs/IAS/article/view/2346}
}
```

## Images

The RIM-ONE DL image dataset consists of 313 retinographies from normal subjects and 172 retinographies from patients 
with glaucoma. These images were captured in three Spanish hospitals: Hospital Universitario de Canarias (HUC), in 
Tenerife, Hospital Universitario Miguel Servet (HUMS), in Zaragoza, and Hospital Clínico Universitario San Carlos 
(HCSC), in Madrid.

This dataset has been divided into training and test sets, with two variants:
- Partitioned randomly: the training and test sets are built randomly from all the images of the dataset. 
- Partitioned by hospital: the images taken in the HUC are used for the training set, while the images taken in the HUMS
  and HCSC are used for testing.

### Download images

The images can be downloaded as a ZIP file from the following link: https://bit.ly/rim-one-dl-images

This ZIP file contains the two variants of the dataset (partitioned randomly and by hospital).


## Reference segmentations of the optic disc and cup

All the images of RIM-ONE DL include a manual segmentation of the disc and cup performed by an expert in glaucoma.

These manual segmentations were carried out using [DCSeg](http://medimrg.webs.ull.es/research/retinal-imaging/glaucoma/).

### Download reference segmentations

The reference segmentations can be downloaded from the following link: https://bit.ly/rim-one-dl-reference-segmentations

This ZIP file contains the segmentation of the disc and cup for each image in PNG format and in DCSeg TXT format.

### Convert DCSeg TXT files to NumPy or PNG

If you would like to use the DCSeg TXT files, in this repository, we have included some Python tools to convert the 
masks generated by DCSeg to NumPy arrays and PNG.

The main file is `generate_dir_binary_masks.py`. This script reads the RIM-ONE DL images and reference segmentations 
directories and converts the TXT masks to PNG, storing the PNG masks in the given output directory. To run the script, 
open it with your editor of choice and adjust the directories and the bottom of the file to point to your actual 
directories.

The previous file makes use of the `dcseg_to_binary_mask` function, which takes the paths to an image and a DCSeg mask 
and returns a NumPy 2D boolean mask.

## CNN Weights

Together with the publication of the RIM-ONE DL database, we described an evaluation benchmark with different models of 
well-known convolutional neural networks, which includes: Xception, VGG16, VGG19, ResNet50, InceptionV3, 
InceptionResNetV2, MobileNet, DenseNet121, NASNetMobile and MobileNetV2.

These networks were trained using the [Keras Deep Learning Framework](https://keras.io/). In every case, the size of the 
input layer was set to 224x224x3, and a GlobalAveragePooling2D layer was added to the convolutional base, followed by a 
fully-connected output layer with two outputs, using SoftMax to distinguish between the Normal and Glaucoma classes.

The following tables show the results achieved by these networks to classify RIM-ONE DL images between Normal and 
Glaucoma classes.

Evaluation of the different networks using the random test set:

Network | AUC | Se | Acc.
------- | --- | -- | ----
VGG19 | 0.9867 | 1.0000 | 0.9315
VGG16 | 0.9834 | 0.9615 | 0.9247
Xception | 0.9771 | 0.9808 | 0.9178
ResNet50 | 0.9755 | 0.9808 | 0.9110
MobileNetV2 | 0.9738 | 0.9423 | 0.9041
DenseNet | 0.9726 | 0.9615 | 0.9041
MobileNet | 0.9712 | 0.9615 | 0.9315
InceptionResNetV2 | 0.9685 | 0.9808 | 0.9110
InceptionV3 | 0.9597 | 0.9423 | 0.8904
NASNetMobile | 0.9290 | 0.9231 | 0.7534


Evaluation of the different networks using the test set partitioned by hospital:

Network | AUC | Se | Acc.
------- | --- | -- | ----
VGG19 | 0.9272 | 0.8750 | 0.8563
VGG16 | 0.9177 | 0.8214 | 0.8506
InceptionV3 | 0.9015 | 0.7500 | 0.8046
Xception | 0.8982 | 0.7500 | 0.7989
DenseNet | 0.8919 | 0.7143 | 0.7816
MobileNet | 0.8912 | 0.7500 | 0.8276
ResNet50 | 0.8855 | 0.7321 | 0.8333
InceptionResNetV2 | 0.8396 | 0.625 | 0.7644
NASNetMobile | 0.7969 | 0.6071 | 0.7989
MobileNetV2 | 0.7765 | 0.4464 | 0.5287


Metrics used in the tables above:
- AUC: Area Under the ROC Curve.
- Se: sensitivity value at a specificity of 0.85
    - `Sensitivity=Tp/(Tp+Fn)`
    - `Specificity=Tn/(Tn+Fp)`
    - where `Tp`, `Fp`, `Tn` and `Fn` are the number of true positives, false positives, true negatives and false 
    negatives, respectively.
- Acc: Accuracy.


### Submit your own results to this page

If you use RIM-ONE DL to train your own method or tune your algorithm and want your results to be published in this 
page, please contact us with the following info:

- Name of your method.
- RIM-ONE DL partition variant used for your method (random or by hospital).
- Results for your method using the 3 metrics described above on the test set of RIM-ONE DL (according to the chosen 
variant).
- Statement where you explicitly confirm that you have only used the training set of RIM-ONE DL to train your method 
(according to the chosen variant). Please note that to keep comparable results among different methods, you should't use 
images from other databases to train your models or tune your algorithms.
- Link to your method's code, description or publication (optional).


### Download CNN Weights

The weights of the CNNs used in the publication can be downloaded from: https://bit.ly/rim-one-dl-cnn-weights

This ZIP file contains the weights in h5 format of each trained network for the two variants of the dataset, i.e. partitioned 
randomly and partitioned by hospital.
