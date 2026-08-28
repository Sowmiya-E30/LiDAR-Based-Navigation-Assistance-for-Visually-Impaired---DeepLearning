A deep learning-based point-cloud processing project for obstacle detection and semantic segmentation using **LiDAR data and Dynamic Graph Convolutional Neural Network (DGCNN)**.

## 📌 Project Overview

This project focuses on using 3D LiDAR point-cloud data to identify and classify objects in the surrounding environment. A DGCNN model is trained to learn geometric relationships between neighboring points and perform point-wise semantic segmentation.

The trained model is evaluated on LiDAR point-cloud data to identify navigation-related objects and simulate obstacle warnings.

## 🎯 Objectives

- Process 3D LiDAR point-cloud data for environment understanding.
- Train a **DGCNN model** for point-cloud semantic segmentation.
- Classify navigation-related objects from LiDAR data.
- Evaluate the trained model using training and validation performance.
- Simulate obstacle detection using the trained model.

## 🧠 Model

The project uses **Dynamic Graph Convolutional Neural Network (DGCNN)**.

DGCNN constructs a dynamic graph from the input point cloud using the **k-Nearest Neighbour (k-NN)** algorithm. In this implementation:

- **k = 20 neighbours**
- Edge features are generated using neighbouring point relationships.
- EdgeConv layers extract local geometric features.
- Features from multiple layers are combined.
- Global features are aggregated and used for point-wise segmentation.

This allows the model to learn spatial and geometric relationships within LiDAR point clouds.

## 📊 Dataset

The project uses processed point-cloud data derived from:

- **ScanNet**
- **PandaSet**

The input data is stored in `.npz` format containing point-cloud coordinates and semantic labels.

### Selected Classes

The model is trained on 12 navigation-related classes:

- Wall
- Floor
- Cabinet
- Chair
- Table
- Door
- Window
- Road
- Sidewalk
- Building
- Vegetation
- Car

Other labels are mapped to an **unknown** class.

## 🔄 Data Preprocessing

The preprocessing pipeline includes:

1. Loading processed `.npz` point-cloud files.
2. Aligning point coordinates with semantic labels.
3. Randomly sampling **1,024 points** from each point cloud.
4. Centering the XYZ coordinates.
5. Normalizing the point cloud using the maximum distance from the center.
6. Applying data augmentation during training.
7. Mapping the original semantic labels to the selected classes.

### Data Augmentation

The training pipeline applies:

- Random rotation
- Random reflection
- Random scaling
- Gaussian noise

These techniques improve the model's ability to generalize to different point-cloud configurations.

## 🧪 Training and Validation

The dataset is divided into training and validation/testing subsets. The model is trained for 100 epochs and evaluated using:

- Training loss
- Validation loss
- Training accuracy
- Validation accuracy

The best model is saved based on the lowest validation loss.

## 📈 Output

The training program generates:

- Training loss curve
- Validation loss curve
- Training accuracy curve
- Validation accuracy curve
- Best trained DGCNN model (`.pth`)
- Point-cloud ground-truth visualizations
- Point-cloud prediction visualizations

Example output structure:
<pre>

dgcnn_simplified_results/
│
├── dgcnn_simplified_best.pth
├── loss_curve.png
├── acc_curve.png
├── simulation_1.png
├── simulation_2.png
├── simulation_3.png
├── simulation_4.png
└── simulation_5.png
</pre>

## 🚨 Obstacle Detection Simulation

After training, the best-performing model is loaded and evaluated on validation samples.

The system identifies objects from the predicted point-cloud classes. Objects such as:

- Person
- Car
- Truck
- Bus
- Motorcycle
- Bicycle

are treated as potentially dangerous objects.

When a dangerous object is detected, the program generates a warning message and can provide voice feedback using `pyttsx3`.

## 🛠️ Technologies Used

- **PyTorch**
- **DGCNN**
- **LiDAR Point Clouds**
- **NumPy**
- **scikit-learn**
- **Matplotlib**
- **PyTorch DataLoader**
- **pyttsx3**
- **CUDA**

## 📁 Project Structure

<pre>
LiDAR-DGCNN-Navigation/
│
├── dgcnn.ipynb
├── README.md
│
├── dataset/
│   └──ScanNet, pandaset/
│
└── results/
    ├── dgcnn_simplified_best.pth
    ├── loss_curve.png
    ├── acc_curve.png
    └── simulation_*.png
</pre>

> Dataset files are not included in this repository because of their size and licensing restrictions.

👨‍💻 Author

Sowmiya E

Btech CSE AI & DS

Project: LiDAR-Based Navigation Assistance for Visually Impaired using DGCNN
