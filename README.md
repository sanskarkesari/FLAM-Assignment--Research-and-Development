# FLAM-Assignment--Research-and-Development
# 📘 Research and Development / AI Assignment

## 🧮 Objective

The objective of this assignment is to estimate the unknown parameters **θ**, **M**, and **X** in the following **parametric curve** equation so that it best fits the given data points in `xy_data.csv`.

\[
x = t\cos(\theta) - e^{M|t|}\sin(0.3t)\sin(\theta) + X
\]

\[
y = 42 + t\sin(\theta) + e^{M|t|}\sin(0.3t)\cos(\theta)
\]

Where:  
- **θ (theta)** = angular rotation (in degrees)  
- **M** = exponential growth/decay factor  
- **X** = horizontal shift  
- **t** = varying parameter, \( 6 < t < 60 \)

---

## ⚙️ Approach and Methodology

### **Step 1 – Data Loading**
The dataset `xy_data.csv` contains the observed **x** and **y** coordinates of points that lie on the curve.

Since the parameter **t** is not provided, it was generated uniformly across the given range:
```python
t = np.linspace(6, 60, len(df))
