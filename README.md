# CelebFace: Deep Learning Flask App for Face Recognition

## Overview

This project focuses on implementing **face detection** and **face recognition** using deep learning models. It leverages a video of Indian Olympic boxer **Mary Kom** to detect and identify faces from selected frames. The models are integrated into a **Flask web application** that allows users to upload images and automatically recognize known faces.

## Key Concepts

* **MTCNN (Multi-task Cascaded Convolutional Network):** Used for detecting face bounding boxes and cropping facial regions.
* **Inception-ResNet V1:** Pre-trained model from `facenet_pytorch` used to generate face embeddings.
* **Face Embeddings:** Numerical representations of facial features that enable comparison between faces.
* **Face Matching:** Comparing embeddings using similarity measures to recognize known faces.
* **Flask Application:** Provides an interactive web interface for users to upload images and perform face recognition in real time.

## Technologies Used

* Python 3
* PyTorch (`facenet_pytorch`)
* OpenCV
* Flask
* NumPy

## Learning Outcomes

* Applying pre-trained deep learning models for computer vision tasks.
* Creating and comparing face embeddings for recognition.
* Building and deploying a simple machine learning app with Flask.

## Author

**Stephen Kinuthia Njoroge**
*Data Science and Machine Learning Enthusiast*
