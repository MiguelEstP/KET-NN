# Quantum Neural Network with Ket

A simple implementation of a **Quantum Neural Network (QNN)** using the **Ket** quantum programming framework. This project explores the fundamentals of Quantum Machine Learning by combining quantum data encoding, variational quantum circuits, and gradient-based optimization for binary classification tasks.

## Overview

This repository implements a Quantum Neural Network capable of learning a simple binary classification problem through:

- Angle encoding of classical data
- Variational quantum circuits (VQC)
- Expectation value measurements
- Gradient-based optimization
- Supervised learning using Mean Squared Error (MSE)

The project serves as an educational introduction to quantum neural networks and variational quantum algorithms.

---

## Architecture

### 1. Data Encoding

Classical features are encoded into quantum states using rotation gates:

\[
|x\rangle = R_Y(x_1) \otimes R_Y(x_2) \otimes \cdots
\]

Each feature is mapped to a qubit through an \(R_Y\) rotation.

### 2. Variational Ansatz

The quantum circuit consists of:

- Parameterized \(R_Y\) gates
- Entangling CNOT operations

Example:

```text
q0 ──RY(w0)──■────
             │
q1 ──RY(w1)──X────
```

The trainable parameters are optimized during training.

### 3. Measurement

After circuit execution, the expectation value of the Pauli-Z operator is measured:

\[
\langle Z_i \rangle
\]

The expectation values are converted into probabilities:

\[
p = \frac{\langle Z \rangle + 1}{2}
\]

which are used for classification.

---

## Loss Function

The model is trained using Mean Squared Error (MSE):

\[
L = \frac{1}{N}
\sum_i
(p_i - y_i)^2
\]

where:

- \(p_i\) is the predicted probability
- \(y_i\) is the target label

---

## Optimization

Gradients are estimated numerically using finite differences:

\[
\frac{\partial z}{\partial \theta}
=
\frac{
z(\theta+\frac{\pi}{2})
-
z(\theta-\frac{\pi}{2})
}{2}
\]

Parameters are updated through gradient descent:

\[
\theta \leftarrow
\theta - \eta \nabla L
\]

where \(\eta\) is the learning rate.

---

## Dataset

A synthetic dataset is generated as follows:

```python
x1, x2 ~ Uniform(0, π)
```

Classification rule:

```python
y = 1 if x1 > x2
y = 0 otherwise
```

Dataset split:

- 75% Training
- 25% Testing

---

## Project Structure

```text
.
├── QNN-KET.ipynb
├── README.md
```

### Main Components

#### QNN

Responsible for:

- Data encoding
- Circuit execution
- Expectation value computation
- Prediction
- Training

#### Optimizer

Responsible for:

- Loss computation
- Gradient estimation
- Parameter updates

---

## Example Usage

```python
qnn = QNN(
    lines=2,
    ansatz=hec_ansatz
)

weights = np.random.randn(2)

weights = qnn.fit(
    X_train,
    Y_train,
    weights,
    epochs=150
)
```

Making predictions:

```python
prediction = qnn.predict(
    x,
    weights
)
```

---

## Technologies

- Python
- NumPy
- Ket Quantum Framework

---

## Future Improvements

- Exact Parameter Shift Rule implementation
- Mini-batch training
- Deeper variational circuits
- Alternative encoding strategies
- Multi-class classification
- PyTorch integration
- Advanced optimizers (Adam, RMSProp)
- Quantum benchmarking against classical models

---

## Learning Goals

This project was developed to explore:

- Quantum Machine Learning (QML)
- Variational Quantum Circuits (VQC)
- Quantum Neural Networks (QNN)
- Expectation-value-based classification
- Gradient optimization in quantum models

---

## Author

**Miguel Estivalet Pinto**

Software Developer and Quantum Computing Student focused on:

- Quantum Computing
- Quantum Machine Learning
- Quantum Neural Networks
- Variational Quantum Eigensolver (VQE)
- Quantum Approximate Optimization Algorithm (QAOA)
