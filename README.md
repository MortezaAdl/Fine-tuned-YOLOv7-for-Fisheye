
# YOLOv7 Fine-Tuning for Fisheye Traffic Scenes

This repository contains the fine-tuned weights of the YOLOv7 model specifically optimized for detecting objects in fisheye traffic scenes. The model has been trained using a unique rotation-augmented training method to enhance its performance on fisheye images captured from an overhead perspective.

## Overview

Conventional object detection algorithms, such as YOLO, struggle to accurately identify objects in fisheye images due to their training on rectilinear images, where objects are usually presented in an upright orientation. Fisheye images can depict objects in various orientations, especially in the lower and central regions, leading to a decline in detection performance. 

To address this challenge, we employed rotation augmentation during the training process, which helps the model generalize better to the diverse orientations of objects seen in overhead fisheye images.

## Key Concepts

### Rotation-Augmented Training

- **Problem**: Traditional CNNs are not rotation-equivariant, causing their performance to suffer when applied to non-upright objects in fisheye images.
- **Solution**: We apply rotation augmentation by including rotated versions of training images to improve the model's robustness and ability to recognize features in different orientations.

### Data Preparation

1. **Dataset**: We used the COCO dataset containing 80 object categories as the base dataset for fine-tuning.
2. **Filtering**:
   - Only images containing at least one road object (Pedestrian, Bike, Car, Motorcycle, Bus, and Truck) were retained.
   - Size-based thresholds were applied to ensure effective training for small objects, as seen by an overhead fisheye camera:
     - 5% for persons, bicycles, and motorcycles
     - 10% for cars
     - 25% for buses and trucks
     - 15% for non-road user objects

*A sample rotated image from the COCO dataset with horizontal bounding boxes
for road objects extracted from rotated segmentation polygons*
<p align="center">
  <img src="https://github.com/user-attachments/assets/3d2090a1-0e74-45fd-adba-078377145086" alt="Sample_COCO">
</p>


### Uniform Rotation Augmentation

To simulate various object orientations, a set of rotation angles is defined for each image:

Angles = { θ + n ⋅ (360° / N) | n ∈ {0, 1, ..., N-1} }

- N is the number of rotations, and θ is a randomly generated angle within [0, 360° / N].
- Each image is rotated around its center, and corresponding annotations are adjusted to fit the new orientations.

*Comparison of the fine-tuned yolov7e6e weights with the original weights and fine-tuned weights on the [FishEye8K](https://github.com/MoyoG/FishEye8K/tree/main) dataset*
![Detection_Results](https://github.com/user-attachments/assets/8ca1899f-440f-4e48-bf99-f489b28b9fd6)

## Usage

1. Clone [YOLOv7](https://github.com/WongKinYiu/yolov7). 
2. Download our fine-tuned weights to the code directory:

      Fine-tuned [yolov7-fisheye](https://drive.google.com/file/d/1Hs6KSQuMZReEjWgKdP4FOO8CMRCxON5T/view?usp=drive_link) weights
      
      Fine-tuned [yolov7e6e-fisheye](https://drive.google.com/file/d/1pN1RuWFBvOzbvpHDHC3qQbLYVlG3G4cl/view?usp=drive_link) weights
   
   Class names: {0:'Pedestrian', 1:'Bike', 2:'Car', 3:'Motorcycle', 4:'Bus', 5:'Truck'}

3. Use the model for inference on overhead fisheye traffic scenes or further fine-tuning.
    


