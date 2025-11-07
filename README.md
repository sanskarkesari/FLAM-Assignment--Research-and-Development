# FLAM-Assignment: Research-and-Development

## 🧮 Objective

The objective of this assignment is to estimate the unknown parameters **θ**, **M**, and **X** in the following **parametric curve** equation so that it best fits the given data points in `xy_data.csv`.

x=tcos(θ)−e^M∣t∣sin(0.3t)sin(θ)+X
y=42+tsin(θ)+e^M∣t∣sin(0.3t)cos(θ)

Where:  
- **θ (theta)** = angular rotation (in degrees)  
- **M** = exponential growth/decay factor  
- **X** = horizontal shift  
- **t** = varying parameter, \( 6 < t < 60 \)

---

## ⚙️ Approach and Methodology


```python
Step 1 – Data Loading

The dataset xy_data.csv contains two columns (x and y).
Since the parameter t was not provided, it was uniformly generated between 6 and 60 using:

t = np.linspace(6, 60, len(df))
This ensures that each point corresponds to an evenly spaced t value.
t = np.linspace(6, 60, len(df))
Step 2 – Defining the Curve

The given mathematical equations were implemented in Python as:

def curve(t, theta, M, X):
    theta_rad = np.deg2rad(theta)
    x_pred = t * np.cos(theta_rad) - np.exp(M * np.abs(t)) * np.sin(0.3 * t) * np.sin(theta_rad) + X
    y_pred = 42 + t * np.sin(theta_rad) + np.exp(M * np.abs(t)) * np.sin(0.3 * t) * np.cos(theta_rad)
    return x_pred, y_pred


This function calculates the predicted (x, y) coordinates for a given set of parameters.

Step 3 – Loss Function (L1 Distance)

The L1 distance was used to measure the difference between the observed and predicted values:
L=i∑​∣xi​−x^i​∣+∣yi​−y^​i​∣
In Python:

def loss(params, t, x_obs, y_obs):
    theta, M, X = params
    x_pred, y_pred = curve(t, theta, M, X)
    return np.sum(np.abs(x_obs - x_pred) + np.abs(y_obs - y_pred))


This ensures the curve fitting process is robust to outliers.

Step 4 – Parameter Optimization

The parameters were optimized using Scipy’s minimize() function with method L-BFGS-B and bounded search space:

initial_guess = [25, 0.0, 50]
bounds = [(0, 50), (-0.05, 0.05), (0, 100)]

result = minimize(loss, initial_guess, args=(t, x_obs, y_obs), bounds=bounds, method='L-BFGS-B
This finds the parameter set that minimizes the L1 distance.

```
📊 Results

After optimization, the following best-fit parameter values were obtained:

| Parameter          | Symbol | Optimal Value |
| ------------------ | ------ | ------------- |
| Angle              | θ      | **28.1187°**  |
| Exponential Factor | M      | **0.02139**   |
| Horizontal Shift   | X      | **54.8998**   |

🧩 Final Parametric Equation: 
x= (tcos(28.1187)−e^0.02139∣t∣sin(0.3t)sin(28.1187)+54.8998
y= 42+tsin(28.1187)+e^0.02139∣t∣sin(0.3t)cos(28.1187))

🏁 Conclusion

The model successfully estimated all unknown parameters.

The L1 distance between predicted and observed points was minimized efficiently.

The resulting curve provides an accurate representation of the dataset.

The project satisfies all evaluation criteria:

✅ L1 Distance Implementation
✅ Process Explanation
✅ Reproducible Code Submission

✨ Credits

Developed by Sanskar Kesari
For the Research and Development / AI Assignment
