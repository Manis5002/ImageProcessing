# GROUP A: 1-MARK QUESTIONS (SHORT ANSWER)

**Degradation Model & Algebraic Formulation:**

**Q. 1. What is the fundamental difference between Image Enhancement and Image Restoration?**
**Main Answer:** **Image Enhancement** is a subjective process aimed at making an image look "better" to a human, whereas **Image Restoration** is an objective, mathematical process aimed at reversing a known physical degradation (like blur) to recover the original true image.

**Q. 2. Write the standard spatial domain equation for the image degradation model.**
**Main Answer:** The spatial domain equation is **$g(x,y) = h(x,y) * f(x,y) + \eta(x,y)$**, where $*$ denotes spatial convolution.

**Q. 3. In the degradation model $g(x,y) = h(x,y) * f(x,y) + \eta(x,y)$, what does $h(x,y)$ represent?**
**Main Answer:** The term **$h(x,y)$** represents the **spatial degradation function** (also known as the Point Spread Function or impulse response), which causes effects like blurring.

**Q. 4. In the degradation model, is the noise typically considered additive or multiplicative?**
**Main Answer:** Noise $\eta(x,y)$ is typically considered to be **additive** and statistically independent of the image coordinates.

**Q. 5. Write the discrete matrix formulation of the degradation model.**
**Main Answer:** The discrete matrix formulation is **$g = Hf + n$**, where $g, f,$ and $n$ are column vectors and $H$ is a block-circulant degradation matrix.

**Q. 6. What is the objective of the unconstrained algebraic approach to image restoration?**
**Main Answer:** The objective is to estimate the original image by simply minimizing the square of the noise norm, **$||n||^2 = ||g - Hf||^2$**, without applying any external conditions or constraints on the image.

**Q. 7. Name the most common filter derived from the unconstrained restoration approach.**
**Main Answer:** The most common filter derived from the unconstrained approach is the **Inverse Filter**.

**Q. 8. What is the major drawback of the Inverse Filter?**
**Main Answer:** The Inverse Filter fails catastrophically in the presence of noise because it **amplifies noise to infinity** at frequencies where the degradation function $H(u,v)$ approaches zero.

**Q. 9. Name one filter derived from the constrained algebraic approach to restoration.**
**Main Answer:** One prominent filter derived from the constrained approach is the **Constrained Least Squares (CLS) Filter** (or Wiener filter).

**Q. 10. In Constrained Least Squares (CLS) restoration, what property of the image is typically minimized?**
**Main Answer:** CLS mathematically minimizes the **second derivative (roughness)** of the image to ensure the restored image remains relatively smooth and free of intense noise spikes.

**Homomorphic & Geometric Transformations:**

**Q. 11. Homomorphic filtering is used to restore images degraded by what type of noise?**
**Main Answer:** Homomorphic filtering is used to restore images degraded by **Multiplicative noise** (like uneven illumination or speckle noise).

**Q. 12. What are the two basic steps involved in geometric transformations?**
**Main Answer:** The two basic steps are **Spatial Transformation** (coordinate mapping) and **Gray-level Interpolation** (assigning pixel intensity values).

**Q. 13. What is a "Tie point" (or Control point) in spatial transformations?**
**Main Answer:** A **Tie point** is a specific pixel whose exact coordinates are known in both the distorted input image and the correct reference image, used to mathematically compute the transformation matrix.

**Q. 14. Name the simplest method of gray-level interpolation.**
**Main Answer:** The simplest method is **Nearest Neighbor Interpolation** (or Zero-order hold).

**Q. 15. Which gray-level interpolation method assigns the gray level of the closest integer coordinate to the transformed pixel?**
**Main Answer:** **Nearest Neighbor Interpolation**.

**Q. 16. Which interpolation method uses the 4 nearest neighbors to compute the gray level of the transformed pixel?**
**Main Answer:** **Bilinear Interpolation**.

**Q. 17. Which interpolation method produces the "blockiest" or most jagged edges?**
**Main Answer:** **Nearest Neighbor Interpolation** produces the most jagged, "blocky" edges (checkerboard effect).

***

# GROUP B: 5-MARK QUESTIONS

**Q. 1. Draw the standard block diagram of the Image Degradation and Restoration process and briefly explain each block.**
**Introduction:**
Image restoration relies on mathematically modeling how an image was corrupted. This model treats degradation as a system operator acting on the original image, followed by the addition of noise.

**Main Answer:**
**Block Diagram:**
```text
                  Noise η(x,y)
                      |
                      v
 f(x,y) ---> [ Degradation ] ---> (+) ---> g(x,y) ---> [ Restoration ] ---> f^(x,y)
Original       Function h(x,y)           Degraded         Filter            Restored
 Image                                    Image           System             Image
```
*   **Original Image $f(x,y)$:** The true, uncorrupted scene.
*   **Degradation Function $h(x,y)$:** The physical distortion (e.g., camera motion blur, out-of-focus lens) mathematically convolved with the image.
*   **Additive Noise $\eta(x,y)$:** Random electrical or sensor noise added to the signal.
*   **Degraded Image $g(x,y)$:** The final corrupted image captured by the camera.
*   **Restoration Filter:** The mathematical algorithm (e.g., Wiener filter) applied to $g(x,y)$ to compute an estimate $\hat{f}(x,y)$ that is as close to $f(x,y)$ as possible.

**Conclusion:**
By perfectly modeling $h(x,y)$ and the statistical properties of $\eta(x,y)$, the restoration filter can effectively run the physical degradation process in reverse.

---

**Q. 2. Formulate the continuous degradation model in both the spatial domain and the frequency domain.**
**Introduction:**
The degradation model assumes that the corruption process is linear and position-invariant (LPI), allowing us to use convolution mechanics.

**Main Answer:**
1.  **Spatial Domain Formulation:**
    In the spatial domain, the degraded image $g(x,y)$ is modeled as the spatial convolution of the true image $f(x,y)$ with a degradation function $h(x,y)$, plus an additive noise term $\eta(x,y)$:
    $$ g(x,y) = h(x,y) * f(x,y) + \eta(x,y) $$
    *(Where $*$ denotes 2D spatial convolution).*
2.  **Frequency Domain Formulation:**
    According to the Convolution Theorem, spatial convolution is mathematically equivalent to multiplication in the frequency domain. Applying the 2D Fourier Transform yields:
    $$ G(u,v) = H(u,v) \cdot F(u,v) + N(u,v) $$
    *(Where $G, H, F,$ and $N$ are the Fourier transforms of $g, h, f,$ and $\eta$ respectively).*

**Conclusion:**
The frequency domain formulation is vastly preferred in restoration because it transforms complex integral calculus (convolution) into simple algebraic multiplication.

---

**Q. 3. Explain the Discrete Formulation of the degradation model ($g = Hf + n$). Briefly explain the dimensions and structure of the vectors and the degradation matrix $H$.**
**Introduction:**
For a computer to process restoration algebraically, the continuous 2D image functions must be converted into 1D discrete mathematical vectors and matrices.

**Main Answer:**
*   **Vector Conversion:** An image of size $M \times N$ is converted into a 1D column vector by stacking its rows end-to-end (lexicographic ordering). 
    *   $f$ (original image), $g$ (degraded image), and $n$ (noise) all become large **column vectors of size $MN \times 1$**.
*   **The Formulation:** The convolution integral is replaced by standard matrix multiplication:
    $$ g = Hf + n $$
*   **The Degradation Matrix $H$:**
    *   $H$ is a massive square matrix of size **$MN \times MN$**.
    *   If an image is $512 \times 512$, $H$ has a staggering $262,144 \times 262,144$ elements.
    *   Because the degradation is assumed to be linear and position-invariant, $H$ is not just a random matrix; it has a highly structured, repetitive pattern known as a **Block-Circulant Matrix**.

**Conclusion:**
While the discrete formulation $g = Hf + n$ provides a perfect algebraic framework for deriving filters, directly inverting the colossal matrix $H$ is computationally impossible, necessitating frequency domain approximations.

---

**Q. 4. What is the Unconstrained Algebraic approach to restoration? How does it lead to Inverse Filtering?**
**Introduction:**
The unconstrained algebraic approach attempts to estimate the original image by relying strictly on the basic degradation equation $g = Hf + n$, without imposing any external rules on what the final image should look like.

**Main Answer:**
*   **Objective:** We want to find an estimate $\hat{f}$ that best explains the degraded image $g$. Since noise $n$ is unknown, the approach mathematically assumes we should minimize the magnitude (norm) of the noise.
*   **Formulation:** We minimize the objective function: 
    $J(\hat{f}) = ||n||^2 = ||g - H\hat{f}||^2$
*   **Derivation:** To find the minimum, we take the derivative of $J$ with respect to $\hat{f}$ and set it to zero:
    $\frac{\partial J}{\partial \hat{f}} = -2H^T(g - H\hat{f}) = 0$
    $H^T H \hat{f} = H^T g$
    Assuming $H$ is an invertible square matrix, this simplifies to:
    **$\hat{f} = H^{-1} g$**
*   **Result:** This derived equation ($\hat{f} = H^{-1} g$) is the mathematical definition of **Inverse Filtering**.

**Conclusion:**
While mathematically sound on paper, the unconstrained approach makes the fatal assumption that minimizing noise variance alone is enough to restore an image, ignoring the instability of $H^{-1}$.

---

**Q. 5. Explain the failure of Inverse Filtering in the presence of noise (especially at high frequencies where $H(u,v)$ approaches zero).**
**Introduction:**
Inverse filtering works perfectly on images with blur but *absolutely zero noise*. However, in real-world scenarios where noise exists, inverse filtering fails spectacularly.

**Main Answer:**
*   **The Mathematical Mechanism:**
    From the frequency domain model $G(u,v) = H(u,v)F(u,v) + N(u,v)$, the inverse filter calculates the estimate $\hat{F}(u,v)$ by simply dividing by $H(u,v)$:
    $$ \hat{F}(u,v) = \frac{G(u,v)}{H(u,v)} = F(u,v) + \frac{N(u,v)}{H(u,v)} $$
*   **The Failure:**
    1.  **High Frequencies:** Physical degradation functions (like blurring) act as low-pass filters. This means their transfer function $H(u,v)$ drops rapidly toward **zero** at high frequencies.
    2.  **Noise Amplification:** Noise $N(u,v)$ usually has a broad spectrum. When we divide $N(u,v)$ by a very small number ($H(u,v) \approx 0$), the term $\frac{N(u,v)}{H(u,v)}$ explodes toward **infinity**.
    3.  **Result:** The amplified noise completely buries the true signal $F(u,v)$. The output image looks like pure, unrecognizable static.

**Conclusion:**
Because it blindly divides by near-zero values, the unconstrained inverse filter is practically useless in the presence of additive noise.

---

**Q. 6. What is the Constrained Algebraic approach? How does it mathematically differ from the unconstrained approach?**
**Introduction:**
To solve the catastrophic noise amplification of the unconstrained inverse filter, researchers developed the **Constrained Algebraic Approach**.

**Main Answer:**
*   **Concept:** Instead of blindly minimizing noise, we force (constrain) the restored image to adhere to a known physical property. A common assumption is that real-world images are mostly smooth.
*   **Mathematical Difference:**
    *   *Unconstrained:* Minimizes $||g - H\hat{f}||^2$ (Only minimizes noise).
    *   *Constrained:* Minimizes the roughness of the image, denoted by $||Q\hat{f}||^2$ (where $Q$ is a linear operator like the Laplacian), **subject to the constraint** that the residual noise must match the known noise variance: $||g - H\hat{f}||^2 = ||n||^2$.
*   **Optimization using Lagrange Multipliers:**
    We combine these into a single Lagrangian objective function:
    $L(\hat{f}, \alpha) = ||Q\hat{f}||^2 + \alpha (||g - H\hat{f}||^2 - ||n||^2)$
    Taking the derivative and setting to zero yields a stable, constrained filter.

**Conclusion:**
By prioritizing image smoothness and treating noise as a known boundary condition rather than a value to be eliminated, constrained approaches (like CLS) produce vastly superior visual results.

---

**Q. 7. Explain the Constrained Least Square (CLS) restoration technique. Why is it considered superior to standard inverse filtering?**
**Introduction:**
The **Constrained Least Squares (CLS)** filter is the direct practical implementation of the constrained algebraic approach, specifically designed to overcome the zero-division flaw of the inverse filter.

**Main Answer:**
*   **Technique:** CLS minimizes the second derivative (the Laplacian) of the image to ensure smoothness. Applying the optimization yields the frequency domain filter:
    $$ \hat{F}(u,v) = \left[ \frac{H^*(u,v)}{|H(u,v)|^2 + \gamma |P(u,v)|^2} \right] G(u,v) $$
    *(Where $\gamma$ is a parameter adjusted to satisfy the noise constraint, and $P(u,v)$ is the Fourier transform of the Laplacian operator).*
*   **Why it is superior:**
    In Inverse Filtering, if $H(u,v) \to 0$, the denominator becomes 0, causing failure. 
    In CLS, if $H(u,v) \to 0$, the denominator becomes **$\gamma |P(u,v)|^2$**. Because the denominator never reaches absolute zero, the noise is never amplified to infinity. Furthermore, CLS only requires the user to know the mean and variance of the noise, whereas filters like Wiener require knowledge of the uncorrupted image's power spectrum.

**Conclusion:**
CLS is mathematically robust and practically feasible, offering a perfect balance between sharpening blurred edges and suppressing amplified noise.

---

**Q. 8. How can Homomorphic Filtering be applied in the context of Image Restoration to eliminate multiplicative noise? Explain with a block diagram.**
**Introduction:**
Standard restoration filters (Inverse, CLS, Wiener) assume noise is **additive**. However, degradations like uneven illumination or radar speckle are **multiplicative** ($g = f \times \eta$). Standard filters fail here.

**Main Answer:**
*   **The Concept:** Homomorphic filtering uses the properties of logarithms to transform the multiplicative degradation model into an additive one, allowing standard linear frequency filtering to be applied.
    $g(x,y) = f(x,y) \cdot \eta(x,y)$
    $\ln(g) = \ln(f) + \ln(\eta)$ -> Now the noise is additive!
*   **Block Diagram:**
```text
 g(x,y) ---> [ ln ] ---> [ DFT ] ---> [ Filter H(u,v) ] ---> [ IDFT ] ---> [ exp ] ---> f^(x,y)
(Multiplicative)        (Frequency       (Separates          (Spatial      (Inverse
                     Domain)          noise & signal)      Domain)       Log)
```
*   **Application:** Illumination varies slowly (low frequency), while image reflectance (edges) varies rapidly (high frequency). A filter $H(u,v)$ is applied to suppress low frequencies and enhance high frequencies. Finally, the exponential function reverses the logarithm to yield the restored image.

---

**Q. 9. What are Geometric Transformations in image restoration? Explain the concept of Spatial Transformation using Affine equations.**
**Introduction:**
While degradation models fix blurring and noise (radiometric distortions), **Geometric Transformations** are required to fix spatial distortions—where the pixels are the right color, but in the wrong physical location (e.g., lens barrel distortion or satellite angle tilt).

**Main Answer:**
*   **Geometric Transformations:** The process of mapping pixels from a distorted spatial grid back to their correct spatial positions to restore the structural geometry of the scene.
*   **Spatial Transformation (Coordinate Mapping):**
    This step calculates the new mathematical coordinate $(x', y')$ for the original pixel $(x,y)$.
    This is commonly modeled using **Affine Transformation Equations**, which can handle translation, rotation, scaling, and shearing simultaneously:
    $$ x' = c_1 x + c_2 y + c_3 xy + c_4 $$
    $$ y' = c_5 x + c_6 y + c_7 xy + c_8 $$
    The coefficients ($c_1$ to $c_8$) are determined by solving a system of linear equations using known "Tie Points". Once solved, every pixel in the distorted image is routed to its corrected $(x', y')$ destination.

---

**Q. 10. Explain Nearest Neighbor Interpolation and Bilinear Interpolation. Compare their visual results on a restored image.**
**Introduction:**
After a spatial transformation routes a pixel to a new coordinate $(x', y')$, the new coordinates are rarely perfect integers (e.g., $x'=4.3, y'=2.8$). Because digital images only exist on integer grids, we must assign a gray-level value using **Interpolation**.

**Main Answer:**
1.  **Nearest Neighbor Interpolation:**
    *   *Concept:* The algorithm simply rounds the fractional coordinate to the closest integer and assigns that pixel's gray level. (e.g., $(4.3, 2.8)$ rounds to $(4, 3)$).
    *   *Visual Result:* Extremely fast to compute, but produces severe **"blocky" or jagged edges** (checkerboard artifacts), especially on straight lines.
2.  **Bilinear Interpolation:**
    *   *Concept:* It looks at the **four nearest integer neighbors** surrounding the fractional coordinate and calculates a weighted average based on how close the fractional point is to each neighbor.
    *   *Visual Result:* Computationally heavier, but produces vastly superior, **smooth edges**. However, because it relies on averaging, the overall restored image may appear slightly blurred compared to the original.

***

# GROUP C: 15-MARK QUESTIONS

### Question 1: Focus on Degradation Model & Unconstrained Approach (7 + 4 + 4)

**(a) Discuss the mathematical model of Image Degradation in the continuous spatial domain. Derive its equivalent frequency domain representation using the Convolution Theorem. (7)**

**Main Answer:**
**Mathematical Model in Spatial Domain:**
Image degradation is modeled as a linear, position-invariant (LPI) system. Let $f(x,y)$ be the continuous uncorrupted image. As it passes through the imaging system, it is subjected to a physical degradation function $h(x,y)$ (e.g., lens blur or motion blur). This process is modeled mathematically as an integral over space, known as **Convolution**. Finally, random additive noise $\eta(x,y)$ (sensor noise) corrupts the signal.
The continuous spatial domain equation is:
$$ g(x,y) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f(\alpha, \beta) h(x-\alpha, y-\beta) d\alpha d\beta + \eta(x,y) $$
Which is shorthand written as:
$$ g(x,y) = h(x,y) * f(x,y) + \eta(x,y) $$

**Frequency Domain Derivation:**
Working with double integrals for restoration is computationally inefficient. We utilize the **Convolution Theorem** of Fourier Transforms, which states that the Fourier transform of a spatial convolution of two functions is simply the point-wise multiplication of their individual Fourier transforms.
1. Take the Fourier transform of both sides of the spatial equation:
   $$ \mathcal{F}\{g(x,y)\} = \mathcal{F}\{h(x,y) * f(x,y) + \eta(x,y)\} $$
2. Because the Fourier transform is a linear operator, it distributes across addition:
   $$ \mathcal{F}\{g(x,y)\} = \mathcal{F}\{h(x,y) * f(x,y)\} + \mathcal{F}\{\eta(x,y)\} $$
3. Apply the Convolution Theorem:
   $$ \mathcal{F}\{g(x,y)\} = \mathcal{F}\{h(x,y)\} \cdot \mathcal{F}\{f(x,y)\} + \mathcal{F}\{\eta(x,y)\} $$
4. Using standard notation ($G, H, F, N$ representing the transforms):
   $$ G(u,v) = H(u,v) F(u,v) + N(u,v) $$
This frequency domain equation forms the fundamental basis for almost all modern image restoration filters.

---

**(b) Derive the Inverse Filter using the Unconstrained Algebraic approach (minimizing the noise term $||n||^2$). (4)**

**Main Answer:**
Using the discrete matrix formulation $g = Hf + n$, the Unconstrained Algebraic approach attempts to find an estimated image $\hat{f}$ by strictly minimizing the noise vector $n$.

1.  **Define Objective Function:** We want to minimize the square of the norm of the noise.
    $$ J(\hat{f}) = ||n||^2 = n^T n $$
    Substitute $n = g - H\hat{f}$:
    $$ J(\hat{f}) = (g - H\hat{f})^T (g - H\hat{f}) $$
2.  **Expand the Equation:**
    $$ J(\hat{f}) = g^T g - g^T H\hat{f} - (H\hat{f})^T g + (H\hat{f})^T (H\hat{f}) $$
    Since $g^T H\hat{f}$ is a scalar, it equals its transpose. The equation simplifies to:
    $$ J(\hat{f}) = g^T g - 2g^T H\hat{f} + \hat{f}^T H^T H \hat{f} $$
3.  **Minimize the Function:** To find the minimum, take the partial derivative of $J$ with respect to $\hat{f}$ and set it to zero:
    $$ \frac{\partial J}{\partial \hat{f}} = -2H^T g + 2H^T H \hat{f} = 0 $$
    $$ H^T H \hat{f} = H^T g $$
4.  **Solve for $\hat{f}$:** Assuming $H$ is a square and invertible matrix, we multiply both sides by $(H^T H)^{-1}$:
    $$ \hat{f} = (H^T H)^{-1} H^T g $$
    $$ \hat{f} = H^{-1} (H^T)^{-1} H^T g = H^{-1} g $$
This result, **$\hat{f} = H^{-1} g$**, is the exact mathematical definition of the **Inverse Filter**.

---

**(c) Prove mathematically why Inverse Filtering amplifies noise and fails drastically when the degradation function $H(u,v)$ has zero or very small values. (4)**

**Main Answer:**
To prove this, we convert the Inverse Filter derivation to the frequency domain. 
The inverse filter calculates the estimate by dividing the degraded image spectrum by the degradation transfer function:
$$ \hat{F}(u,v) = \frac{G(u,v)}{H(u,v)} $$
We know the mathematical model of the degraded image is $G(u,v) = H(u,v)F(u,v) + N(u,v)$. Substituting this into the inverse filter equation:
$$ \hat{F}(u,v) = \frac{H(u,v)F(u,v) + N(u,v)}{H(u,v)} $$
$$ \hat{F}(u,v) = F(u,v) + \frac{N(u,v)}{H(u,v)} $$

**Proof of Failure:**
1.  **The True Signal:** The first term is exactly $F(u,v)$, which means if there is zero noise ($N=0$), the filter perfectly recovers the original image.
2.  **The Noise Term:** The second term dictates the failure. Physical blurring acts as a low-pass filter, meaning its transfer function $H(u,v)$ rapidly approaches **zero** at high frequencies.
3.  **Amplification:** As $H(u,v) \to 0$, the mathematical fraction $\frac{N(u,v)}{H(u,v)}$ approaches **infinity**. 
Therefore, at higher frequencies, the noise term completely overpowers the true image signal $F(u,v)$, destroying the restored image with massive, high-amplitude noise static.

***

### Question 2: Focus on Constrained Restoration & CLS (7 + 4 + 4)

**(a) What is the Constrained Algebraic approach to restoration? Formulate the objective function (minimizing $||Qf||^2$ subject to $||g - Hf||^2 = ||n||^2$) and explain the role of the Lagrange multiplier. (7)**

**Main Answer:**
**Concept:**
The Constrained Algebraic approach addresses the fatal noise amplification of inverse filtering by introducing prior knowledge about the image. Instead of only minimizing noise, it imposes a structural constraint on the solution—typically that real-world images are continuous and visually "smooth".

**Formulation:**
Let $Q$ be a linear operator (usually the Laplacian) that measures the roughness (high-frequency edges/noise) of an image. The goal is to find an image estimate $\hat{f}$ that minimizes this roughness:
*   **Minimize:** $||Q\hat{f}||^2$
However, we cannot minimize roughness to zero, or the image would just be a flat gray box. The estimate must still mathematically satisfy the degradation model. Thus, we impose a strict constraint:
*   **Subject to:** $||g - H\hat{f}||^2 = ||n||^2$ (The residual error must exactly equal the variance of the known sensor noise).

**The Role of the Lagrange Multiplier:**
To solve this constrained optimization problem, we combine both equations using a **Lagrange Multiplier ($\alpha$)** to form a single Lagrangian objective function:
$$ L(\hat{f}, \alpha) = ||Q\hat{f}||^2 + \alpha \left( ||g - H\hat{f}||^2 - ||n||^2 \right) $$
By differentiating this equation with respect to $\hat{f}$ and setting it to zero, the Lagrange multiplier $\alpha$ forces the optimization algorithm to strike a mathematically perfect balance between keeping the image smooth and keeping the image faithful to the degraded observation.

---

**(b) Detail the Constrained Least Squares (CLS) filtering approach. Write down the frequency domain transfer function for the CLS filter. (4)**

**Main Answer:**
The **Constrained Least Squares (CLS)** filter is the direct frequency-domain realization of the Lagrangian optimization derived above. It is specifically designed to handle additive noise robustly without requiring full knowledge of the image's power spectrum (unlike the Wiener filter).

When we differentiate the Lagrangian equation $L(\hat{f}, \alpha)$ and solve for $\hat{f}$, we obtain the following matrix solution:
$$ \hat{f} = (H^T H + \gamma Q^T Q)^{-1} H^T g $$
*(Where $\gamma = 1/\alpha$)*

To avoid impossible matrix inversions, we map this solution directly to the frequency domain. The **CLS Transfer Function** becomes:
$$ \hat{F}(u,v) = \left[ \frac{H^*(u,v)}{|H(u,v)|^2 + \gamma |P(u,v)|^2} \right] G(u,v) $$
*   $H^*(u,v)$ is the complex conjugate of the degradation function.
*   $P(u,v)$ is the Fourier transform of the 2D Laplacian operator (representing the roughness constraint $Q$).
*   $\gamma$ is the regulatory parameter.

Because the denominator contains $\gamma |P(u,v)|^2$, it never approaches absolute zero, mathematically curing the noise amplification problem of the inverse filter.

---

**(c) How is the parameter $\gamma$ (gamma) estimated/adjusted in Constrained Least Squares restoration? (4)**

**Main Answer:**
The parameter $\gamma$ is a scaling weight that controls how strongly the smoothness constraint is enforced. It is not guessed; it is mathematically iteratively estimated to satisfy the noise constraint $||g - H\hat{f}||^2 = ||n||^2$.

**Estimation Steps:**
1.  Define a residual vector: $r = g - H\hat{f}$.
2.  We want the magnitude of the residual $||r||^2$ to equal the known noise variance $||n||^2$.
3.  Define a function $\phi(\gamma) = ||r(\gamma)||^2 - ||n||^2$. Our goal is to find $\gamma$ such that $\phi(\gamma) \approx 0$ (within a small tolerance error $a$).
4.  **Iterative Process:**
    *   Choose an initial value for $\gamma$.
    *   Compute the filter and calculate the new residual $||r||^2$.
    *   If $||r||^2 > ||n||^2 + a$, the image is too smooth. Decrease $\gamma$ and re-filter.
    *   If $||r||^2 < ||n||^2 - a$, the image is too noisy. Increase $\gamma$ and re-filter.
5.  This loop repeats until the condition is met, automatically optimizing the restoration filter for the specific image.

***

### Question 3: Focus on Discrete Formulation & Homomorphic Restoration (7 + 4 + 4)

**(a) Explain the Discrete Formulation of the degradation model. Detail how 2D image matrices $f$ and $g$ are converted into 1D column vectors and how the impulse response $h$ forms a massive block-circulant matrix $H$. (7)**

**Main Answer:**
To process image restoration computationally, the continuous spatial integral must be formulated as discrete linear algebra matrices.

**1. Conversion to 1D Column Vectors:**
An image $f(x,y)$ captured by a computer is a discrete 2D matrix of size $M \times N$. To formulate the equation $g = Hf + n$, we must convert the 2D matrices $f$, $g$, and $n$ into 1D column vectors.
This is done via **Lexicographic Ordering** (Row-stacking). The first row of the image forms the top of the vector, the second row is stacked directly underneath it, and so on. 
The resulting vectors $f, g,$ and $n$ have the colossal dimension of **$MN \times 1$**.

**2. The Block-Circulant Matrix $H$:**
Because the 2D images have been unrolled into massive 1D vectors, the degradation function $h(x,y)$ must be expanded into an operator capable of acting on them. 
This operator becomes $H$, a massive matrix of dimension **$MN \times MN$**.
*   Because the degradation is Position-Invariant (the blur is the same everywhere in the image), the rows of $H$ are simply shifted versions of the row above it. This makes $H$ a **Circulant Matrix**.
*   Because the image was unrolled row-by-row, $H$ is constructed of smaller sub-matrices that are themselves circulant. Therefore, $H$ is officially classified as a **Block-Circulant Matrix**.
This highly predictable structure allows $H$ to be diagonalized by the Discrete Fourier Transform, which is the entire theoretical foundation for frequency-domain filtering.

---

**(b) Most standard degradation models assume additive noise. Explain how Homomorphic Filtering transforms a multiplicative degradation model (e.g., $g(x,y) = f(x,y) \times \eta(x,y)$) into an additive one. (4)**

**Main Answer:**
Standard restoration filters (like Inverse or Wiener) rely heavily on the Fourier Transform. The Fourier Transform is a linear operator, meaning it cannot separate components that have been multiplied together. If an image suffers from multiplicative noise, applying a standard filter directly will fail.

**The Transformation:**
Homomorphic filtering bypasses this by utilizing the mathematical properties of **Logarithms**.
1.  Start with the multiplicative model: $g(x,y) = f(x,y) \cdot \eta(x,y)$
2.  Take the Natural Logarithm ($\ln$) of both sides of the equation.
3.  By the logarithmic product rule ($\ln(a \cdot b) = \ln(a) + \ln(b)$), the equation becomes:
    $$ \ln[g(x,y)] = \ln[f(x,y)] + \ln[\eta(x,y)] $$
By simply passing the image through a logarithmic operator, the multiplicative noise has been successfully transformed into **additive noise**, allowing standard, linear frequency-domain filters to be applied to separate and remove it.

---

**(c) Outline the steps to restore an image suffering from uneven illumination using homomorphic filtering. (4)**

**Main Answer:**
Uneven illumination is a multiplicative degradation ($g = illumination \times reflectance$). 
**Steps for Homomorphic Restoration:**
1.  **Logarithmic Transform:** Apply $\ln$ to the degraded image $g(x,y)$ to separate the illumination and reflectance components additively.
2.  **Fourier Transform:** Apply the Fast Fourier Transform (FFT) to shift the logged image into the frequency domain. Illumination forms the low-frequency components, and reflectance forms the high-frequency components.
3.  **High-Frequency Emphasis Filter:** Apply a specialized Homomorphic Filter transfer function $H(u,v)$ that heavily attenuates (compresses) the low frequencies and amplifies the high frequencies. This eliminates the bad lighting while sharpening the object details.
4.  **Inverse Fourier Transform:** Apply the IFFT to bring the filtered image back to the spatial domain.
5.  **Exponential Transform:** Apply the $\exp()$ function (the inverse of the natural log) to reverse the original mathematical shift and retrieve the final, perfectly illuminated image.

***

### Question 4: Focus on Geometric Transformations & Interpolation (6 + 5 + 4)

**(a) Geometric transformation consists of two basic operations: Spatial Transformation and Gray-level Interpolation. Explain both concepts clearly. (6)**

**Main Answer:**
Geometric transformations do not fix brightness or blur; they fix physical, spatial distortions in an image, such as an angled photo of a document or a fisheye lens curve.

**1. Spatial Transformation (Coordinate Mapping):**
This operation physically moves a pixel from its distorted location to its correct physical location. It is defined mathematically by transformation equations. For a pixel at original coordinates $(x,y)$, a set of Affine equations mathematically calculates its new, corrected destination coordinates $(x', y')$.
*   $x' = r(x,y)$ and $y' = s(x,y)$
This corrects the structural geometry of the scene.

**2. Gray-level Interpolation:**
When the spatial transformation calculates the new coordinate $(x', y')$, the resulting numbers are almost always fractions (e.g., $x'=4.7, y'=2.1$). However, digital image grids only possess whole-integer pixels (e.g., Pixel $(4,2)$ or $(5,2)$).
Gray-level interpolation is the mathematical process of estimating and assigning an appropriate gray-level brightness value to these non-integer destination coordinates based on the known brightness values of the surrounding integer pixels.

---

**(b) Detail the mathematical formulation of Bilinear Interpolation. How does it calculate the unknown pixel value using its four nearest neighbors? (5)**

**Main Answer:**
**Bilinear Interpolation** assigns a gray-level value to a fractional coordinate $(x,y)$ by looking at its **four nearest integer neighbors** and computing a weighted average.

**Mathematical Formulation:**
The gray level $v(x,y)$ at the fractional coordinate is modeled by the bilinear equation:
$$ v(x,y) = ax + by + cxy + d $$

**Calculation Process:**
1.  The algorithm identifies the four integer coordinate pixels immediately surrounding the fractional point $(x,y)$.
2.  Since the gray levels $v$ of these four integer neighbors are known, we can set up a system of four linear equations using the formula above.
3.  The system solves for the four unknown coefficients: $a, b, c,$ and $d$.
4.  Once the coefficients are calculated, they are plugged back into the original equation $v(x,y) = ax + by + cxy + d$ to calculate the final, exact gray-level value for the fractional pixel.

This results in a smooth, highly accurate color transition, entirely eliminating the blocky artifacts seen in simpler interpolation methods.

---

**(c) Discuss "Tie Points" (Control points). How are they used to model spatial transformations when the exact mathematical distortion function is unknown? (4)**

**Main Answer:**
In real-world scenarios, the exact mathematical function that caused an image to warp (e.g., atmospheric distortion on a satellite) is completely unknown. We solve this using **Tie Points**.

**Concept & Usage:**
1.  **Identification:** A Tie Point is a distinct, easily recognizable feature (like the corner of a building or a road intersection) whose exact pixel coordinates are known in *both* the distorted image $(x,y)$ and a perfectly accurate reference image $(x',y')$.
2.  **Modeling the Transformation:** We assume the distortion can be modeled by Affine equations (which require 8 unknown coefficients, $c_1$ to $c_8$).
    $$ x' = c_1 x + c_2 y + c_3 xy + c_4 $$
    $$ y' = c_5 x + c_6 y + c_7 xy + c_8 $$
3.  **Solving:** Because each Tie Point gives us a known $x, y, x',$ and $y'$, it provides two equations. By selecting **4 distinct Tie Points**, we generate 8 equations. Using linear algebra, we solve for the 8 unknown coefficients.
4.  **Application:** Once the coefficients are known, the mathematical transformation matrix is complete and can be applied to re-map every other pixel in the entire image to its correct location.

***

### Question 5: Mixed Conceptual Bag (5 + 5 + 5)

**(a) Compare and contrast Image Enhancement with Image Restoration. Give one practical example of a degradation that requires restoration rather than mere enhancement. (5)**

**Main Answer:**
| Feature | Image Enhancement | Image Restoration |
| :--- | :--- | :--- |
| **Objective** | To make an image visually pleasing for human analysis. | To reverse physical degradation and recover the mathematical original. |
| **Nature of Process** | Highly **Subjective** (Heuristic). | Highly **Objective** (Mathematical). |
| **Prior Knowledge** | Requires zero prior knowledge of the image or camera. | Strictly requires prior mathematical modeling of the degradation function (PSF) and noise. |
| **Techniques Used** | Contrast stretching, Histogram equalization. | Inverse filtering, Wiener filter, CLS. |

**Practical Example:**
**Linear Motion Blur.** If a camera shutter is open while a car speeds past, the resulting image has directional motion blur. Enhancement techniques (like sharpening or contrast stretching) will only amplify the streaking and noise. True recovery requires **Restoration**—specifically using an inverse filter mathematically modeled to the exact speed and angle of the car to de-convolve the blur and retrieve the license plate number.

---

**(b) Compare Nearest Neighbor, Bilinear, and Bicubic interpolation in terms of computational complexity and resulting image quality (blurring vs. jaggedness). (5)**

**Main Answer:**
1.  **Nearest Neighbor (Zero-order hold):**
    *   *Complexity:* Lowest. It requires zero math, simply rounding the decimal coordinate to the nearest integer.
    *   *Quality:* Poorest. It produces severe jaggedness and blocky "checkerboard" artifacts, especially on diagonal edges. No blurring occurs.
2.  **Bilinear Interpolation:**
    *   *Complexity:* Medium. It solves a linear equation using the 4 surrounding neighbors.
    *   *Quality:* Good. It completely eliminates jagged edges, creating smooth transitions. However, the averaging process introduces a slight, noticeable **blurring** across the image.
3.  **Bicubic Interpolation:**
    *   *Complexity:* Highest. It fits a complex 3D cubic spline surface using the **16 nearest neighbors**.
    *   *Quality:* Exceptional. It is the industry standard for commercial software (like Photoshop). It perfectly balances sharpness and smoothness, eliminating blockiness without suffering from the heavy blurring of bilinear interpolation.

---

**(c) Write a short note on the Wiener Filter (Minimum Mean Square Error filter) as a practical implementation of the constrained algebraic approach. (5)**

**Main Answer:**
The **Wiener Filter**, formally known as the Minimum Mean Square Error (MMSE) filter, is the gold standard of image restoration. It incorporates both the degradation function and the statistical characteristics of noise to restore an image optimally.

*   **Objective:** Unlike Inverse filtering which minimizes noise, the Wiener filter minimizes the mean square error between the estimated image $\hat{f}$ and the actual true image $f$:
    **$e^2 = E[(f - \hat{f})^2]$**
*   **Transfer Function:** The frequency domain formulation is:
    $$ \hat{F}(u,v) = \left[ \frac{H^*(u,v)}{|H(u,v)|^2 + \frac{S_\eta(u,v)}{S_f(u,v)}} \right] G(u,v) $$
    *(Where $S_\eta$ is the power spectrum of the noise, and $S_f$ is the power spectrum of the original uncorrupted image).*
*   **Practicality:** The Wiener filter brilliantly balances de-blurring and noise suppression. If noise is zero ($S_\eta = 0$), the formula mathematically collapses into the standard Inverse Filter. If noise is incredibly high, the ratio dominates the denominator, heavily suppressing the noise rather than amplifying it to infinity.
