<div align="center">
<h1>
<b>
MLP Corrected Distance Estimation for Non Horizontal Camera Measurements
</b>
</h1>
</div>

When the camera is installed non-horizontally relative to the target object, issues such as angle variations and inconsistent distance measurements for multiple reference points on the same object make it challenging to establish a uniform safety distance. Therefore, in this experiment, a GUI is developed using [PyQt5](https://pypi.org/project/PyQt5/). The [Intel RealSense D435i](https://www.intelrealsense.com/depth-camera-d435i/) is employed to capture both images and distance measurements. Once the camera is securely positioned, users can create a simple dataset by capturing images and setting the current vertical distance from the camera. By moving left and right to capture data, the coordinates (X, Y) of each point within the entire bounding box, along with the Z coordinate captured by the camera, are used as inputs. The output is the horizontal distance from the camera.

| GUI Design| Scene Illustration | 
|---|---|
| ![image](https://github.com/KennyChen880127/MLP-Corrected-Distance-Estimation-for-Non-Horizontal-Camera-Measurements/blob/main/example_1.png) | ![image](https://github.com/KennyChen880127/MLP-Corrected-Distance-Estimation-for-Non-Horizontal-Camera-Measurements/blob/main/example_2.png) |

## Multilayer Perceptron (MLP)

[Multilayer Perceptron (MLP)](https://en.wikipedia.org/wiki/Multilayer_perceptron) is a type of artificial neural network designed for supervised learning. It consists of multiple layers of nodes, or neurons, organized in a feedforward manner. The network is composed of an input layer, one or more hidden layers, and an output layer.In MLP, each connection between nodes is assigned a weight, and each node within the network applies an activation function to the weighted sum of its inputs. The layers between the input and output are known as hidden layers, and they contribute to the network's ability to learn complex patterns and representations.MLP is versatile and has been successfully applied to various tasks, including classification, regression, and pattern recognition. Its flexibility and ability to capture non-linear relationships make it a popular choice for solving complex problems in machine learning and artificial intelligence.

## Features
Through the use of a for loop, we can obtain each key point of the human body's pose one by one. We calculate the distances between each pair of coordinates, and use statistical methods like [Quartile](https://en.wikipedia.org/wiki/Quartile) to identify and handle outlier values. Finally, for the coordinates corresponding to these outlier values, we perform calculations to determine the appropriate adjustments. This approach helps address the issue of key points extending beyond the body's boundaries and enhances the accuracy of pose estimation.
  
### Training
First, you need to choose a simple image as a calibration reference. You can refer to the [training process of YOLOv8](https://docs.ultralytics.com/modes/train/), and you also have the option to use pre-trained YOLOv8 weights from one of the 80 classes in the COCO dataset, selecting a category with a relatively large area.

Through the "Record Data" button in the GUI, the system will capture the current XYZ coordinates along with the inputted horizontal distance. The data will be stored in Notepad format, adhering to the following specifications:
| X | Y | Z | HD |
|---|---|---|---|
| 406 | 368 | 175.8 | 120.0 |
| 452 | 322 | 167.7 | 130.0 |
| 525 | 411 | 235.3 | 140.0 |
| 491 | 310 | 232.6 | 150.0 |
| 592 | 305 | 205.6 | 160.0 |
| 584 | 329 | 214.8 | 170.0 |

Where X and Y represent the coordinates on the screen, Z corresponds to the measured distance captured by the camera at point (X, Y), and HD denotes the horizontal distance.

### Predicting
After completing the training, you can make predictions using the following command:

        python predict.py
