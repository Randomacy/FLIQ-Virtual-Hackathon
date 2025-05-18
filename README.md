# QUAIL: Quantum Understanding and AI for Interpretability and Learning

*A hybrid quantum-classical model for interpretable drug-induced autoimmunity prediction.*

## 🧬 Introduction

Drug-induced autoimmunity (DIA) is a complex phenomenon where pharmaceuticals trigger autoimmune reactions. Predicting which compounds are likely to induce DIA is a critical challenge in drug discovery and safety assessment.

This project explores whether quantum-enhanced machine learning (QML) can improve prediction accuracy and interpretability using RDKit-derived molecular descriptors.

## ⚛️ Our Approach

We developed a hybrid model combining classical neural networks with a Variational Quantum Algorithm (VQA) using 2–4 qubits. Our architecture:

- Compresses 196 chemical descriptors to 2 features via a classical linear layer
- Feeds them into a parameterized quantum circuit with entanglement and trainable gates
- Outputs predictions using a final classical layer

We also implemented **quantum-native interpretability** using input perturbation (MIFI-style) to rank which features most influence quantum circuit outputs.

## 🧰 Tools & Technologies

- Python, PyTorch, Qiskit 2.x
- StandardScaler for normalization
- StatevectorEstimator as the quantum backend
- Custom PyTorch `autograd.Function` to enable end-to-end training with quantum layers
- Plotly + ipywidgets for interactive dashboarding

## 📊 Exploratory Data Analysis

- 477 molecules with 196 RDKit descriptors + binary DIA label
- Mostly sparse or binary-like features (e.g., `fr_urea`, `fr_benzene`)
- Class imbalance: [Mildly skewed / Balanced] distribution
- Top features visualized using Random Forest baseline
- PCA confirmed partial class separation in reduced space

