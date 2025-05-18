# QUAIL: Quantum Understanding and AI for Interpretability and Learning

*A hybrid quantum-classical model for interpretable drug-induced autoimmunity prediction.*

## 🧬 Introduction

Drug-induced autoimmunity (DIA) is a complex phenomenon where pharmaceuticals trigger autoimmune reactions. Predicting which compounds are likely to induce DIA is a critical challenge in drug discovery and safety assessment.

This project explores whether quantum-enhanced machine learning (QML) can improve prediction accuracy and interpretability using RDKit-derived molecular descriptors.

## ⚛️ Our Approach

We developed a hybrid model combining classical neural networks with a Variational Quantum Algorithm (VQA) using 2–6 qubits. Our architecture:

- Compresses 196 chemical descriptors to 2-6 features via a classical linear layer
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

## Data Preprocessing
- Features normalized using StandardScaler.-
- Optionally, PCA is applied to reduce dimensionality from 196 → 2 for qubit feasibility.

## Classical Modeling (Baseline)
We evaluated traditional models for reference:
- Logistic Regression: Fast convergence, low recall on minority class.
- Random Forest: Best classical performance with feature importance.

This provided a benchmark for accuracy and F1-score to compare against the quantum model.

## Quantum Modeling with VQC
We implemented a hybrid quantum-classical neural network architecture:
- A classical linear layer reduces 196 descriptors to 2-6 features.
- These 2-6 features are encoded as qubit angles via a ZZFeatureMap.
- A parameterized ansatz (e.g., RealAmplitudes) acts as a quantum processing layer.
- Final classical layers map quantum outputs to DIA predictions.

Training is done using StatevectorEstimator and a custom autograd.Function to enable gradient-based learning.

Despite working with only 2–6 qubits, the model had decent outcomes.

## Quantum Explainability via IPA
This is where our approach is most unique.

We implement Input Perturbation Attribution (IPA) for quantum models:
- We perturb each PCA-reduced feature by a small angle (e.g., π/8).
- We observe the resulting change in quantum prediction probabilities.
- This gives us a feature importance score per PCA dimension.

To map this back to the original RDKit descriptors, we:
- Take the absolute loading weights of the PCA components.
- Multiply them by IPA scores to project attribution back into the full descriptor space.
- Finally, we visualize the top contributing chemical descriptors to the quantum model's predictions.

# tl;dr
In this work, we present a novel hybrid quantum-classical pipeline that combines Variational Quantum Classifiers (VQCs) with Input Perturbation Attribution (IPA) and Principal Component Analysis (PCA) to extract interpretable insights from quantum models. By training a VQC on PCA-reduced features derived from high-dimensional RDKit molecular descriptors, we make quantum modeling feasible under current qubit limitations. We then apply IPA to estimate feature influence within the quantum decision process, and project those scores back to the original chemical descriptors to recover domain-relevant explanations. This layered interpretability framework offers a rare window into the inner workings of quantum machine learning models, providing practical attribution while maintaining end-to-end hybridization. To our knowledge, this combination of VQC + IPA + PCA back-projection has not been previously demonstrated in existing QML tutorials or literature.
