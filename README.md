# YOLOv8 Car Make-Model Classification

This repository contains the code and documentation for training a YOLOv8 model to classify car make and model using a provided dataset. The project also includes model inference, conversion to TensorRT (INT8 precision), and deployment using FastAPI. Additionally, the repository includes Docker setup for containerized deployment.

Project Overview
This project is part of a coding test that involves several key tasks:

1. Dataset Preparation:
   - Organizing and preprocessing a dataset of car images labeled with their make and model.
   - Splitting the dataset into training and validation sets.
     
3. Model Training:
   - Training a YOLOv8 classification model on the car make-model dataset.
   - Fine-tuning the model with techniques such as data augmentation to achieve optimal accuracy.

4. Model Inference:
   - Implementing a function to classify new car images using the trained YOLOv8 model.
   - Displaying the results of the classification.

5. Model Conversion to TensorRT (INT8 Precision):
   - Converting the trained YOLOv8 model to TensorRT with INT8 precision for optimized inference performance.
