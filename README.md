# Road Segment Analysis for ADAS (RS-ADAS)

<p float="left">
  <img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/input_video.gif" width="49%" style="margin-right: 2%;" />
  <img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/output_video.gif" width="49%" />
</p>


## Introduction
RS-ADAS is an advanced analytical tool designed to enhance Autonomous Driving Assistant Systems by providing precise road segmentation capabilities. Leveraging the Segment Anything Model (SAM), RS-ADAS is capable of accurately differentiating road surfaces from their surroundings under various conditions, including urban, suburban, and rural environments.

## Project Description
The project employs a two-stage process involving YOLOv8 for initial road detection and SAM for subsequent road segmentation. The RS-ADAS system is trained on a vast array of environments, allowing for a comprehensive understanding and interaction with different road types, improving the decision-making process in ADAS.

## Technologies Used
- **YOLOv8**: Employs advanced object detection to identify road areas within images, marking them with bounding boxes.
- **Segment Anything Model (SAM)**: Provides high-fidelity segmentation of the detected road areas, separating them from other elements in the image.

## Project Workflow
<img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/RS-SAM%20FLOWCHART.png" weight="20%">

- **Image Acquisition**: Images of various environments are first processed through the YOLOv8 object detection model.
- **Road Detection**: YOLOv8 analyzes the images to detect the road and provides bounding boxes around the detected road area.
- **Segmentation**: The detected road areas are then passed to SAM, which precisely segments the road from the rest of the image.
- **Output**: The final output is a segmented image highlighting the road, ready for use by ADAS for navigation and decision-making.

## YOLOv8 Object Detection Architecture Overview
![U-Net Architecture with VGG Backbone](https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/yolo.jpg)
This image illustrates the detailed architecture of the YOLOv8 object detection model. It is a comprehensive schematic that outlines the flow from input image to detected objects.

### Backbone Architecture
The backbone is responsible for feature extraction and is constructed using a series of convolutional layers:

- **Pyramid Scaling Layers (P1 - P5)**: These layers form a feature pyramid that captures a wide range of object sizes and details.
- **CSPDarknet Layers**: Central to the backbone, they process the input images through a series of convolutions and shortcut connections.
- **C2F Blocks**: These are cross-stage partial blocks that enhance feature fusion by combining low and high-level information.
- **SPPF (Spatial Pyramid Pooling - Fast)**: This block pools features at different spatial scales to capture contextual information effectively.

### Head Architecture
The head is where the actual detection takes place and is comprised of:

- **YOLOv8 Detection Heads**: These are present for each scale (P3, P4, P5) and are responsible for predicting bounding boxes, objectness scores, and class probabilities.
- **Convolutional Layers**: They are used to process the feature maps and refine the detection results.
Upsampling Layers: These layers are utilized to merge feature maps from different levels of the backbone.
- **Loss Functions**: Includes Binary Cross-Entropy (BCE) for class prediction and Complete Intersection over Union (CIoU) loss for bounding box accuracy.
  
### Detection Process Details
- **Bottleneck and Concatenation**: Bottleneck layers followed by concatenation steps ensure rich feature maps that combine multiple levels of information.
- **Batch Normalization and SiLU Activation**: Included within convolutional blocks to stabilize learning and introduce non-linearities.
- **Detect Layers**: Located at strategic points in the architecture, they interpret the refined feature maps to make final object predictions.


### Dataset Composition

- **Training Set**: 5,000 images with corresponding segmentation masks.
- **Testing Set**: 1,00 images with associated masks for model accuracy evaluation.

### Preprocessing Techniques

- **Resizing**: Uniformly resized images and masks to 640 x 640 x 3 to standardize the input data.
- **Normalization**: Applied normalization to standardize pixel values across all images and eliminate outliers.

### Training Infrastructure

- Conducted on **Amazon SageMaker** with an NVIDIA Tesla T4 GPU (ml.g5.2xlarge instance).

### Training Hyperparameters

- **Epochs**: 100 epochs to balance learning and prevent overfitting.
- **Batch Size**: A batch size of 16, optimizing memory usage and model performance.
- **Learning Rate**: Set to 0.0001 for steady convergence without overshooting minima.
- **Custom Loss Function**: Binary Cross Entropy
- **Primary Metric**: Accuracy was used to gauge predictive performance.
- **Callbacks**: Early Stopping with a patience of 12 epochs and model checkpointing to save the best-performing model iteration.

<p float="left">
  <img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/input_video.gif" width="49%" style="margin-right: 2%;" />
  <img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/output_video_box.gif" width="49%" />
</p>

## SAM Segmentation
- The SAM model takes the detected road area and performs detailed segmentation, isolating the road with high precision.

<p float="left">
  <img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/output_video_box.gif" width="49%" style="margin-right: 2%;" />
  <img src="https://github.com/AnanthaPadmanaban-KrishnaKumar/RS-SAM/blob/main/assets/output_video.gif" width="49%" />
</p>

## Key Features
- **Versatile Segmentation**: Capable of handling diverse environmental conditions.
- **Real-Time Processing**: Though computationally intensive, efforts are being made to optimize the model for real-time applications.
- **Adaptive Learning**: Constantly improves from new data, enhancing its segmentation capabilities over time.

## Applications

RS-ADAS finds its use in various domains:

- **Autonomous Vehicle Navigation**: Assists self-driving vehicles in path detection and navigation.
- **Traffic Management Systems**: Aids in the design and control of traffic systems.
- **Urban and Rural Planning**: Offers insights into road conditions for urban and rural development.

## Drawbacks
A current limitation of RS-ADAS is the high time complexity from input to output, which impacts its feasibility for real-time applications. The intricate processing required for accurate segmentation increases computational demands, leading to longer processing times.

## Future Directions
Efforts are underway to optimize RS-ADAS for real-time processing without compromising the accuracy of road detection and segmentation, aiming to make it viable for live autonomous vehicle applications.

## Conclusion:
RS-ADAS stands as a testament to the potential of combining YOLOv8's detection capabilities with the segmentation prowess of SAM, offering a promising solution to the challenges of road detection in ADAS. While there are hurdles to overcome, particularly concerning processing speed, the system's adaptability and precision set the stage for future enhancements and broader application.
