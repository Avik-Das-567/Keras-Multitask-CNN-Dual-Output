# Keras Multitask CNN Dual Output

A deep learning project demonstrating **multi-task learning using Keras Functional API**, where a single Convolutional Neural Network (CNN) simultaneously learns two tasks from the same input: **digit classification** and **synthetic color prediction**.

This implementation showcases how to design **multi-output architectures with shared representations**, enabling efficient learning across related tasks.

---

## Overview

This project builds a **multi-output neural network** that takes an MNIST image as input and produces:

- **Digit classification output** (0–9)
- **Color classification output** (synthetic label generated from input data)

The model leverages:
- Shared convolutional feature extraction layers
- Task-specific output heads
- A **skip connection (ResNet-style)** to improve gradient flow and representation learning

The architecture is implemented using the **Keras Functional API**, allowing flexible graph-based model design beyond sequential constraints.

---

## Model Architecture

The model follows a **shared backbone + branching heads** design:

### Shared Feature Extractor
- Convolutional layers for spatial feature extraction
- Non-linear activations
- Feature map transformation into a shared latent representation

### Skip Connection
- A residual-style connection is introduced using `Add`
- Helps preserve lower-level features and stabilize training

### Task-Specific Heads

1. **Digit Classification Head**
   - Fully connected layers
   - Softmax activation
   - Output: 10 classes

2. **Color Classification Head**
   - Parallel dense layers
   - Softmax activation
   - Output: synthetic color labels

---

## Data Pipeline

### Dataset
- Based on the **MNIST dataset**
- Input: grayscale handwritten digit images

### Custom Data Generation

A custom function (`generate_data`) is used to:
- Assign **synthetic color labels** to each image
- Create a **multi-label dataset**
- Return inputs along with two corresponding targets

This transforms a single-task dataset into a **multi-task learning setup**.

---

## Learning Paradigm

### Multi-Task Learning

The model is trained to optimize **two objectives simultaneously**:

- Digit classification loss
- Color classification loss

Each task contributes to the overall loss, encouraging the model to learn:
- Shared representations useful across tasks
- Task-specific refinements via separate output heads

---

## Training Strategy

### Loss Functions
- Separate categorical losses applied to each output
- Combined during training

### Optimization
- Gradient-based optimization (via Keras/TensorFlow backend)
- Backpropagation flows through both shared and task-specific layers

### Callbacks

The training process includes:
- **Custom Logger callback**
  - Tracks and prints performance metrics
- **TensorBoard integration**
  - Enables visualization of:
    - Loss curves
    - Training progression

---

## Model Outputs

The model produces two predictions per input:

| Output Type        | Description                     |
|-------------------|---------------------------------|
| Digit Prediction   | Recognizes the digit (0–9)      |
| Color Prediction   | Predicts assigned color label   |

These outputs demonstrate how a single network can handle **multiple learning objectives concurrently**.

---

## Evaluation & Visualization

The notebook includes:
- Sample predictions
- Visualization of model outputs
- Comparison between true and predicted labels

This helps validate:
- Task performance
- Generalization capability
- Effectiveness of shared learning

---

## Key Concepts Demonstrated

- Keras Functional API for non-linear architectures
- Multi-output model design
- Multi-task learning
- Shared representation learning
- Residual/skip connections in CNNs
- Custom data pipeline creation
- Training with multiple loss functions
- Model monitoring with TensorBoard

---

## Learning Objectives Achieved

- Designing and implementing **multi-task neural networks**
- Training models with **multiple outputs and objectives**
- Understanding how shared layers improve learning efficiency
- Applying architectural techniques like **skip connections**
- Moving beyond sequential models to **graph-based model design**

---

## Summary

This project serves as a practical implementation of **multi-task deep learning**, illustrating how a single CNN can be extended to solve multiple related problems efficiently. By combining shared feature extraction with task-specific outputs, it highlights a foundational approach used in more advanced systems such as object detection and multi-modal learning models.
