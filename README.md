# YOLOv8 Car Make-Model Classification

This repository contains the code and documentation for training a YOLOv8 model to classify car make and model using a provided dataset. The project also includes model inference, conversion to TensorRT (INT8 precision). Additionally, the repository includes Docker setup for containerized FastAPI deployment.

## Project Overview
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

## How to Run the code

1. Clone the Repository
```
git clone https://github.com/hafizsam/CarMake-Classifier
cd CarMake-Classifier
```

2. Setup the Environment:
```
pip install ultralytics
```

3. Train the Model:
Use the training script or notebook to train the YOLOv8 model on the provided dataset.

4. Run Inference:
Use the inference script to classify new car images and view the results.

5. Convert to TensorRT:
Run the TensorRT conversion script to optimize the trained model for deployment.

## How to run fastAPI of yolov8 model using docker image
1. Pull the FastAPI Docker Image from Docker Hub:
If there's an existing FastAPI Docker image on Docker Hub that you want to use, you can pull it using the docker pull command. For example, if you want to use an image named tiangolo/uvicorn-gunicorn-fastapi, you would run:

```
docker pull hafizsam/yolo-classify-app:v1.0
```
This pulls the specified image version to your local machine.

2. Prepare Your FastAPI Application:
Ensure that your FastAPI application is ready to be served. You would have your FastAPI app in a file named app.py, but you can adjust this according to your setup.

3. Run the Docker Container:
You can run your FastAPI application by mounting your local directory containing the FastAPI code into the Docker container. Here's how to do it:

```
docker run -d --name myfastapiapp -p 8000:80 -v $(pwd):/app hafizsam/yolo-classify-app
```
Here's a breakdown of this command:

 - -d: Runs the container in detached mode (in the background).
 - --name yolo-classify-app:yolo-classify-app Names the container myfastapiapp.
 - -p 8000:80: Maps port 8000 on your local machine to port 80 inside the Docker container. FastAPI, using Uvicorn, will serve on port 80 by default in this image.
 - -v $(pwd):/app: Mounts your current directory (where your FastAPI code resides) into the /app directory in the container. This allows the container to access your FastAPI code.
 - hafizsam/yolo-classify-app: The Docker image you're using, which you previously pulled from Docker Hub.

4. Access the FastAPI Application:
After running the container, your FastAPI application should be accessible at http://localhost:8000 in your web browser.
Interactive API documentation is available at http://localhost:8000/docs (Swagger UI).

## Model Conversion to TensorRT
Objective: Convert the trained YOLOv8 model to TensorRT for optimized inference, focusing on deploying the model with INT8 precision for better performance on NVIDIA hardware.

### Challenges Encountered

1. Calibration for INT8 Precision:
**Challenge**: INT8 precision requires calibration to ensure that the model maintains accuracy after quantization.
**Solution**: Used a representative dataset (data="car_model") during the export process for calibration. This dataset provided the necessary range of input data to correctly calibrate the model, ensuring minimal loss in accuracy.

2. Memory Constraints:
**Challenge**: Running the TensorRT engine with large batch sizes or insufficient workspace memory could lead to out-of-memory errors.
**Solution**: Adjusted the batch size and workspace parameters to balance performance with available GPU memory. For example, setting batch=8 and workspace=4 GB worked well in this case.

3. Loading and Inference Issues:
**Challenge**: Loading the TensorRT engine and running inference might fail if the engine is not compatible with the hardware or if the file path is incorrect.
**Solution**: Utilized Google Colab ensured that the TensorRT engine was built on the same hardware or a compatible environment where it will be deployed. Also, double-checked the file paths to ensure the engine file was correctly referenced.

4. Performance Optimization:
**Challenge**: Optimizing the TensorRT model for both speed and accuracy, especially when using INT8 precision.
**Solution**: Fine-tuned the calibration process to achieve a good balance between inference speed and model accuracy.

### Conclusion
The process of converting the YOLOv8 model to TensorRT with INT8 precision resulted in a significant improvement in inference speed, making the model highly suitable for deployment in real-time applications. However, this increase in speed came at the cost of some accuracy. The reduction in precision was a trade-off necessary to meet the performance requirements, particularly in scenarios where speed is critical. The challenges, particularly around INT8 calibration, were addressed through careful tuning of the export parameters and by using a representative calibration dataset to minimize the impact on accuracy.
