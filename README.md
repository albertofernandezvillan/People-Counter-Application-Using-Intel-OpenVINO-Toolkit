# Deploying a People Counter App at the Edge

The people counter application demonstrates how to create a smart video IoT solution using Intel® hardware and software tools. The app will detect people in a designated area, providing the number of people in the frame, average duration of people in frame, and total count. This project is a part of Intel Edge AI for IOT Developers Nanodegree program by udacity.


![screenshot_1](https://user-images.githubusercontent.com/34116562/80679006-ab9dc000-8ad9-11ea-9756-1fdb898276b2.png)


### How it works?

The counter will use the Inference Engine included in the Intel® Distribution of OpenVINO™ Toolkit. The model used should be able to identify people in a video frame. The application should count the number of people in the current frame, the duration that a person is in the frame (time elapsed between entering and exiting a frame) and the total count of people. It then sends the data to a local web server using the Paho MQTT Python package.


![architectural diagram](./images/arch_diagram.png)


## Requirements

#### Hardware

* 6th to 10th generation Intel® Core™ processor with Iris® Pro graphics or Intel® HD Graphics.
* OR use of Intel® Neural Compute Stick 2 (NCS2)

#### Software

*   Intel® Distribution of OpenVINO™ toolkit 2019 R3 release
*   Node v6.17.1
*   Npm v3.10.10
*   CMake
*   MQTT Mosca server
*   Python 3.5 or 3.6
  
  
### Explaining Model Selection & Custom Layers
 
TensorFlow Object Detection Model Zoo (https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md) contains many pre-trained models on the coco dataset. Ssd_inception_v2_coco and faster_rcnn_inception_v2_coco performed good as compared to rest of the models, but, in this project, faster_rcnn_inception_v2_coco is used which is fast in detecting people with less errors. Intel openVINO already contains extensions for custom layers used in TensorFlow Object Detection Model Zoo.

Downloading the model from the GitHub repository of Tensorflow Object Detection Model Zoo by the following command:

```
wget http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
```
Extracting the tar.gz file by the following command:

```
tar -xvf faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
```
Changing the directory to the extracted folder of the downloaded model:

```
cd faster_rcnn_inception_v2_coco_2018_01_28
```
The model can't be the existing models provided by Intel. So, converting the TensorFlow model to Intermediate Representation (IR) or OpenVINO IR format. The command used is given below:

```
python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model faster_rcnn_inception_v2_coco/frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --reverse_input_channels --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/faster_rcnn_support.json
```

### Comparing Model Performance


### Model Use Cases


### Effects on End user needs


### Running the Main Application
