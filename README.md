
# YOLOv7 Fine-Tuning for Fisheye Traffic Scenes

This repository contains the fine-tuned weights of the YOLOv7 model specifically optimized for detecting objects in fisheye traffic scenes. The model has been trained using a unique rotation-augmented training method to enhance its performance on fisheye images captured from an overhead perspective.

## Overview

Conventional object detection algorithms, such as YOLO, struggle to accurately identify objects in fisheye images due to their training on rectilinear images, where objects are usually presented in an upright orientation. Fisheye images can depict objects in various orientations, especially in the lower and central regions, leading to a decline in detection performance. 

To address this challenge, we employed rotation augmentation during the training process, which helps the model generalize better to the diverse orientations of objects seen in overhead fisheye images.

## Key Concepts

### Rotation-Augmented Training

- **Problem**: Traditional CNNs are not rotation-equivariant, causing their performance to suffer when applied to non-upright objects in fisheye images.
- **Solution**: We apply rotation augmentation by including rotated versions of training images to improve the model's robustness and its ability to recognize features in different orientations.

### Data Preparation

1. **Dataset**: We used the COCO dataset, which contains 80 object categories, as the base dataset for fine-tuning.
2. **Filtering**:
   - Only images containing at least one road object were retained.
   - Size-based thresholds were applied to ensure effective training for objects as seen by an overhead fisheye camera:
     - 5% for persons, bicycles, and motorcycles
     - 10% for cars
     - 25% for buses and trucks
     - 15% for non-road user objects

### Uniform Rotation Augmentation

To simulate various object orientations, a set of rotation angles is defined for each image:

Angles = { θ + n ⋅ (360° / N) | n ∈ {0, 1, ..., N-1} }

- N is the number of rotations, and \(\theta\) is a randomly generated angle within \([0, \frac{360^\circ}{N})\).
- Each image is rotated around its center, and corresponding annotations are adjusted to fit the new orientations.

## Usage

1. Download the fine-tuned weights:

      Fine-tuned [yolov7](https://drive.google.com/file/d/1Hs6KSQuMZReEjWgKdP4FOO8CMRCxON5T/view?usp=drive_link) weights
      
      Fine-tuned [yolov7e6e](https://drive.google.com/file/d/1pN1RuWFBvOzbvpHDHC3qQbLYVlG3G4cl/view?usp=drive_link) weights

2. Use the model for inference on fisheye images or further fine-tuning as required.

## Acknowledgments

- The COCO dataset is used as a base for fine-tuning the model, and we acknowledge its creators.
- Special thanks to the developers of YOLOv7 for providing a robust framework for object detection.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
