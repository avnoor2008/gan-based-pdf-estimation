# GAN-Based Non-Parametric PDF Estimation

This project demonstrates the use of a **Generative Adversarial Network (GAN)** to learn the **probability density function (PDF)** of a transformed variable using **samples only**, without assuming any analytical or parametric distribution.

The input variable is derived from **NO₂ concentration** values from an air quality dataset.

---

## Transformation Parameters

The original variable \( x \) is transformed using the nonlinear function:

\[
z = T(x) = x + a_r \sin(b_r x)
\]

Where:
- **Roll Number:** 102317198
- \( r = (102303830 \bmod 5) + 1 = 1 \)
- \( a_r = 0.5 \times r = 0.5 \)
- \( b_r = 0.3 \times r = 0.3 \)

---

## GAN Architecture Description

A **one-dimensional GAN** is used to model the distribution of the transformed variable \( z \).

### Generator
- Input: Random noise vector (dimension = 5)
- Fully connected layers with ReLU activation
- Output: Synthetic samples approximating the real data distribution

### Discriminator
- Input: Scalar value (real or generated \( z \))
- Fully connected layers with ReLU activation
- Sigmoid output for real/fake classification

The networks are trained adversarially using **Binary Cross-Entropy loss** and the **Adam optimizer**.

---

## PDF Obtained from GAN Samples

<p align="center">
  <img width="740" height="362"
       alt="PDF estimated from GAN samples"
       src="https://github.com/user-attachments/assets/bb424691-1117-487e-b5d6-585125e06e56" />
</p>

After training, a large number of samples are generated from the generator.  
The probability density function (PDF) is estimated using **Histogram Density Estimation** and **Kernel Density Estimation (KDE)**.

---

## Interpretation of Results

### PDF Characteristics
- The learned distribution is **unimodal and left-skewed**, with most probability mass concentrated around **negative values of \( z \)**.
- This behavior is consistent with the **nonlinear sinusoidal transformation** applied to normalized NO₂ concentration data.
- The KDE curve smoothly follows the histogram, indicating a **stable and coherent approximation** of the underlying distribution.

---

## Observations

### Mode Coverage
- The generator captures the **dominant mode** of the transformed distribution.
- No evidence of **mode collapse** is observed.
- Sample spread around the mode reflects effective learning of data variability.

### Training Stability
- Generator and discriminator losses remain **bounded and well-balanced**.
- Discriminator loss fluctuates around **1.3–1.4**, while generator loss stabilizes between **0.67 and 0.82**.
- Training progresses smoothly without divergence.

### Quality of Generated Distribution
- The generated samples form a **smooth and realistic PDF**.
- Central tendency and variance are well preserved.
- Minor tail smoothing is observed, which is expected given finite training epochs and low-dimensional model capacity.

---

## Conclusion

The GAN successfully learns an **implicit, non-parametric representation** of the probability density of the transformed NO₂ variable using **samples alone**, without assuming any analytical or parametric form.

---

## Author

Avnoor Kamboj
