# Experimental Training

# Our Pretrained Model

## Age Classification

<img src="https://github.com/abars/YoloKerasFaceDetection/blob/master/pretrain/log/agegender_age_miniXception.png" width="50%" height="50%">

<http://www.abars.biz/keras/agegender_age_miniXception.hdf5>

<http://www.abars.biz/keras/agegender_age_miniXception.prototxt>

<http://www.abars.biz/keras/agegender_age_miniXception.caffemodel>

## Gender Classification

<img src="https://github.com/abars/YoloKerasFaceDetection/blob/master/pretrain/log/agegender_gender_simple_cnn.png" width="50%" height="50%">

<http://www.abars.biz/keras/agegender_gender_simple_cnn.hdf5>

<http://www.abars.biz/keras/agegender_gender_simple_cnn.prototxt>

<http://www.abars.biz/keras/agegender_gender_simple_cnn.caffemodel>

## Face Detection

<http://www.abars.biz/keras/yolov2-face.h5>

<!--
<http://www.abars.biz/keras/fddb_yolosmallv1_final.weights>

<https://github.com/abars/YoloKerasFaceDetection/blob/master/cfg/fddb_yolosmallv1.cfg>

<http://www.abars.biz/keras/fddb_yolosmallv1.prototxt>

<http://www.abars.biz/keras/fddb_yolosmallv1.caffemodel>

## Hand Detection

<http://www.abars.biz/keras/vivahand_tinyyolov1_19000.weights>

<https://github.com/abars/YoloKerasFaceDetection/blob/master/vivahand_tinyyolov1.cfg>
-->

# Install

## Modify Darknet

Download Darknet and put in the same folder.

https://github.com/pjreddie/darknet

Compile with <https://github.com/abars/YoloKerasFaceDetection/blob/master/darknet_custom/yolo.c> for custom classes and custom cfg.

`void train_yolo(char *cfgfile, char *weightfile,const char *train_images,const char *backup_directory)`

`draw_detections(im, l.side*l.side*l.n, thresh, boxes, probs, voc_names, alphabet, l.classes);`

`int class = find_int_arg(argc, argv, "-class", 20);`

`char *train_images = find_char_arg(argc, argv, "-train", 0);`

`char *backup_directory = find_char_arg(argc, argv, "-backup", 0);`

`else if(0==strcmp(argv[2], "train")) train_yolo(cfg, weights, train_images, backup_directory);`

`else if(0==strcmp(argv[2], "demo")) demo(cfg, weights, thresh, cam_index, filename, voc_names, class, frame_skip, prefix, out_filename);`

# Face Detection (Widerface)

## Create dataset

Download wider face dataset (wider_face_split and WIDER_train folder) and put in the dataset/widerface folder.

http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/

Create dataset/widerface/WIDER_train/annotations_keras folder for keras.

`perl annotation_widerface_keras.pl`

Create datase/widerface/WIDER_train/annotations_darknet folder for darknet.

`perl annotation_widerface_darknet.pl`

## Train using Darknet

Here is a train.

`cd darknet`

`./darknet yolo train ../cfg/widerface_tinyyolov1.cfg -train ../dataset/widerface/WIDER_train/annotations_darknet/train.txt -backup ./backup/ -class 1`

## Train using Keras

Download BasicYoloKeras and put in the same folder.

https://github.com/experiencor/basic-yolo-keras

Here is a train.

`cd basic-yolo-keras-master`

`python train.py -c ../cfg/widerface_keras.json`

##  Test using Darknet

Here is a test.

`./darknet yolo test ../cfg/widerface_tinyyolov1.cfg ./backup/widerface_tinyyolov1_4000.weights ../dataset/widerface/WIDER_train/annotations_darknet/1.jpg -class 1`

Here is a run.

`./darknet yolo demo ../cfg/widerface_tinyyolov1.cfg ./backup/widerface_tinyyolov1_4000.weights -class 1`

## Convert to Caffe Model

Download pytorch-caffe-darknet-convert and put in the same folder.

https://github.com/marvis/pytorch-caffe-darknet-convert

Convert to Caffe model.

`cd pytorch-caffe-darknet-convert`

`python darknet2caffe.py ../cfg/fddb_yolosmallv1.cfg ./backup/fddb_yolosmallv1_36000.weights face.prototxt face.caffemodel`

# Emotion classification

## Create Dataset

Download FER2013 dataset.

https://www.kaggle.com/c/challenges-in-representation-learning-facial-expression-recognition-challenge/data

## Train

Implementing.

