# QUANTUM-ENHANCED-CLUSTERING-OF-LA-ICP-MS-GEOCHEMICAL-DATA-USING-QCNN
# Quantum-Enhanced Clustering of LA-ICP-MS Geochemical Data (HQCNN)

Hybrid quantum–classical pipeline for clustering high-dimensional LA-ICP-MS geochemical datasets using a PennyLane-based variational quantum circuit (VQC) + classical layers, compared against K-Means with Silhouette scoring. :contentReference[oaicite:0]{index=0}

---

## 🚀 Overview
- **Problem:** LA-ICP-MS datasets are high-dimensional (30–60 elements/sample), compositional (closed-sum), and multicollinear—classical clustering often struggles on such data. :contentReference[oaicite:1]{index=1}
- **Solution:** Centered log-ratio (CLR) transform → standardize → **PCA to 4 components** → 4-qubit VQC with CZ entanglement → classical head → cluster labels; evaluated vs **K-Means** using Silhouette scores and manifold visualizations (PCA/t-SNE). :contentReference[oaicite:2]{index=2}
- **Stack:** Python, PennyLane `default.qubit`, NumPy, scikit-learn, Matplotlib/Seaborn. Hardware-ready for IBM Q / Xanadu with minimal changes. :contentReference[oaicite:3]{index=3}

---

## ✨ Key Contributions
- **HQCNN architecture**: quantum feature mapping via a 4-qubit VQC (RY init → CZ chain → trainable RY) producing a nonlinear 4D quantum feature vector. :contentReference[oaicite:4]{index=4}  
- **Geochemically aware preprocessing**: CLR to handle closed-sum compositional effects, then PCA for decorrelation and dimensionality reduction. :contentReference[oaicite:5]{index=5}  
- **Benchmarking**: Compared quantum-enhanced clusters against classical K-Means using Silhouette score, plus visual diagnostics (2D/3D PCA, t-SNE). :contentReference[oaicite:6]{index=6}

---

## 🧱 Architecture

```text
Raw LA-ICP-MS ppm → CLR → Standardize → PCA (k=4)
      ↓
  Encode to 4 qubits (RY angles from PCA features)
      ↓
   CZ entanglement chain + trainable RY
      ↓
⟨Z⟩ on each qubit → 4D quantum features
      ↓
  Classical dense layer → cluster labels
