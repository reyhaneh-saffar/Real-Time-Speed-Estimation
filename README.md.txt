# Real Time Speed Estimation Using Optical Flow and Deep Learning

## Introduction
This project aims to estimate vehicle speeds from video sequences captured in urban environments, a task with real-world applications in autonomous driving, traffic analysis, and road safety. The approach integrates:
1. **Optical Flow Estimation**: Utilizing RAFT (Recurrent All-Pairs Field Transforms) to capture motion between video frames.
2. **Speed Prediction**: Using Convolutional Neural Networks (CNNs) to predict vehicle speed from the computed optical flow.

---

## Methodology

### Step 1: Optical Flow Estimation
**Why RAFT?**  
RAFT was chosen for its robustness and ability to handle large displacements and brightness changes, making it well-suited for urban driving scenarios.

**Key Steps**:
- **Frame Preparation**: Extracted consecutive frames from video sequences.
- **Model Setup**: Used RAFT pre-trained on the KITTI dataset for optical flow computation.
- **Flow Visualization**: Generated HSV visualizations to interpret pixel-wise motion.

Optical flow images provided a strong representation of motion patterns, serving as the input for speed prediction models.

---

### Step 2: Speed Prediction Using CNNs
**Data Preprocessing**:
- Resized optical flow images to 224x224 and normalized using ImageNet statistics.
- Paired preprocessed flow images with speed labels for training and testing datasets.

**Model Architectures**:
1. **ResNet18**: Adapted for regression with a single-output linear layer. Known for robust feature extraction.
2. **EfficientNet-B0**: Modified similarly, offering a compact and efficient design.

**Training Setup**:
- **Loss Function**: Mean Squared Error (MSE) for speed regression.
- **Optimizer**: Adam with a learning rate of 0.001.
- **Hardware**: GPU acceleration for both training and inference.

---

## Results

### Training Performance
- **ResNet18**: Demonstrated steady loss reduction across 12 epochs, with a final training loss of ~0.46.
- **EfficientNet**: Training was more unstable, concluding with a final training loss of ~4.12 after 10 epochs.

### Test Performance
- **ResNet18**: Achieved a mean test loss of ~0.69, reflecting high accuracy.
- **EfficientNet**: Test loss was ~1.55, indicating lower accuracy and stability.
