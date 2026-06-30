# GROUP A: 1-MARK QUESTIONS (SHORT ANSWER)

**Domains & Contrast Enhancement:**

**Q. 1. What is the fundamental difference between the Spatial Domain and the Frequency Domain in image enhancement?**
**Main Answer:** The **Spatial Domain** involves direct manipulation of the image pixels, whereas the **Frequency Domain** involves mathematically transforming the image (using Fourier Transform), modifying its frequency components, and taking the inverse transform.

**Q. 2. What is Contrast Stretching?**
**Main Answer:** **Contrast Stretching** is a piecewise linear spatial domain technique that expands the narrow range of intensity levels in an image to span the full dynamic range of the display device.

**Q. 3. Name a non-linear contrast stretching transformation.**
**Main Answer:** Two common non-linear contrast stretching transformations are the **Log Transformation** and the **Power-Law (Gamma) Transformation**.

**Q. 4. What is Gamma Correction (Power-Law Transformation)?**
**Main Answer:** **Gamma Correction** is a non-linear operation ($s = c \cdot r^\gamma$) used to correct the power-law response phenomena of display devices, stretching or compressing dark/light regions depending on whether $\gamma < 1$ or $\gamma > 1$.

**Q. 5. If an image is extremely dark, where will the components of its histogram be concentrated?**
**Main Answer:** For an extremely dark image, the histogram components will be heavily concentrated on the **lower (left) end** of the gray-scale axis.

**Q. 6. What is the main objective of Histogram Equalization?**
**Main Answer:** The main objective of **Histogram Equalization** is to produce an output image with a perfectly **uniform (flat) histogram**, thereby automatically maximizing the global contrast of the image.

**Spatial Smoothing & Sharpening:**

**Q. 7. Write the mask (kernel) for a standard $3 \times 3$ spatial mean (average) filter.**
**Main Answer:** The standard $3 \times 3$ mean filter mask is:
$$ \frac{1}{9} \begin{bmatrix} 1 & 1 & 1 \\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{bmatrix} $$

**Q. 8. What is the primary application of a spatial low-pass filter?**
**Main Answer:** The primary application of a spatial low-pass filter is **Image Smoothing (Blurring)** and the reduction of random additive **noise**.

**Q. 9. How does increasing the size of an averaging mask (e.g., from $3 \times 3$ to $5 \times 5$) affect an image?**
**Main Answer:** Increasing the mask size increases the degree of blurring, which suppresses more noise but also causes a severe **loss of fine detail and sharper edge degradation**.

**Q. 10. Image averaging is used to eliminate which type of noise?**
**Main Answer:** Image averaging is primarily used to eliminate **Zero-mean random additive noise**, such as Gaussian noise.

**Q. 11. What is the primary purpose of Image Sharpening?**
**Main Answer:** The primary purpose of **Image Sharpening** is to highlight fine details and enhance abrupt spatial transitions (edges) that have been previously blurred.

**Q. 12. Does a high-pass filter enhance or suppress the low-frequency components (background/smooth areas)?**
**Main Answer:** A high-pass filter **suppresses** the low-frequency components (the smooth background areas) while allowing the high-frequency components (edges) to pass.

**Q. 13. Write the standard $3 \times 3$ spatial mask for a Laplacian filter (second-order derivative).**
**Main Answer:** A standard $3 \times 3$ Laplacian mask is:
$$ \begin{bmatrix} 0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0 \end{bmatrix} $$

**Q. 14. State the formula for High-boost filtering in terms of the original image and the low-pass filtered image.**
**Main Answer:** The formula for High-boost filtering is: **$Highboost = A \cdot (Original \ Image) - (Lowpass \ Image)$**, where $A > 1$.

**Q. 15. Which derivative (first or second) produces thicker edges?**
**Main Answer:** The **First-order derivative** (e.g., Sobel) produces **thicker edges**, whereas the second-order derivative (e.g., Laplacian) produces much finer, sharper, and thinner double-edges.

**Frequency Domain & Homomorphic Filtering:**

**Q. 16. Name the mathematical transform used to convert an image from the spatial domain to the frequency domain.**
**Main Answer:** The **Discrete Fourier Transform (DFT)** is used.

**Q. 17. What causes the "Ringing Effect" (or Gibbs phenomenon) in frequency domain filtering?**
**Main Answer:** The Ringing Effect is caused by the **sharp, abrupt cutoff** (the "brick-wall" transition) of an Ideal Low Pass Filter (ILPF) in the frequency domain, which manifests as ripples in the spatial domain.

**Q. 18. Which frequency domain low-pass filter does not exhibit the ringing effect?**
**Main Answer:** The **Gaussian Low Pass Filter (GLPF)** does not exhibit any ringing effect because its inverse Fourier transform is also a smooth Gaussian curve.

**Q. 19. What is the specific purpose of Homomorphic Filtering?**
**Main Answer:** The specific purpose of **Homomorphic Filtering** is to simultaneously **compress the dynamic range** (by suppressing illumination) and **enhance the contrast** (by amplifying reflectance).

**Q. 20. In homomorphic filtering, what mathematical operation is applied first to separate illumination and reflectance?**
**Main Answer:** The **Natural Logarithm ($\ln$)** is applied first to convert the multiplicative illumination and reflectance components into an additive linear sum.

***

# GROUP B: 5-MARK QUESTIONS

**Q. 1. Differentiate between Spatial Domain and Frequency Domain enhancement techniques.**
**Introduction:**
Image enhancement can be performed in two fundamentally different mathematical spaces: the Spatial Domain and the Frequency Domain.

**Main Answer:**
| Feature | Spatial Domain Enhancement | Frequency Domain Enhancement |
| :--- | :--- | :--- |
| **Operation Target** | Direct manipulation of the physical **pixels** of the image $f(x,y)$. | Manipulation of the **Fourier Transform** (frequency coefficients) $F(u,v)$ of the image. |
| **Mathematical Basis** | Relies heavily on **Convolution** using spatial masks/kernels. | Relies on point-by-point **Multiplication** of the image transform and the filter transfer function. |
| **Computational Complexity** | Generally faster and computationally simpler for small filter masks ($3\times3$). | Computationally expensive due to the need for forward and inverse Fast Fourier Transforms (FFT). |
| **Primary Use Cases** | Contrast stretching, Histogram equalization, basic blurring/sharpening. | Precise filtering (Ideal, Butterworth), Homomorphic filtering, removing periodic noise. |

**Conclusion:**
While spatial domain techniques are highly intuitive and fast for localized enhancements, the frequency domain provides unparalleled precision for analyzing and manipulating global image characteristics like periodicity and sharp transitions.

---

**Q. 2. Explain Linear Contrast Stretching with the help of a transformation curve (graph). How does it improve a low-contrast image?**
**Introduction:**
Low-contrast images result from poor illumination or improper aperture settings, causing the pixel values to clump tightly together. **Linear Contrast Stretching** is a spatial enhancement technique that resolves this.

**Main Answer:**
*   **Concept:** Contrast stretching is a piecewise linear transformation that expands a narrow range of intensity levels in the input image to span the full dynamic range of the output display (e.g., $0$ to $255$).
*   **Improvement Mechanism:** By mapping the darkest pixel in the image to absolute black ($0$) and the brightest pixel to absolute white ($255$), the visual separation between features is maximized, drastically improving clarity.

**Diagram: Transformation Curve**
```text
 Output (s)
 255 |                     /------- (r2, 255)
     |                    /
     |                   / 
     |                  /  <-- Stretched Range
     |                 /
     |                /
     |  (r1, 0)------/
     |
     +--------------------------------- Input (r)
        0          r1    r2          255
```
*   *Explanation:* Values below $r_1$ are forced to $0$ (black). Values above $r_2$ are forced to $255$ (white). The narrow range between $r_1$ and $r_2$ is linearly stretched to span the entire $0-255$ scale.

---

**Q. 3. Discuss non-linear contrast stretching. Explain the Log Transformation and Power-Law (Gamma) transformation with their respective transfer curves.**
**Introduction:**
While linear stretching applies constant changes, **non-linear contrast stretching** expands or compresses different ranges of gray levels by varying degrees to reveal hidden details.

**Main Answer:**
1.  **Log Transformation ($s = c \log(1+r)$):**
    *   *Function:* It greatly expands the narrow values of dark pixels while severely compressing the higher values of bright pixels.
    *   *Application:* Used extensively to display the Fourier transform spectrum, which usually contains a massive dynamic range that cannot be displayed directly.
2.  **Power-Law / Gamma Transformation ($s = c \cdot r^\gamma$):**
    *   *Function:* The effect depends entirely on the value of $\gamma$.
        *   If $\gamma < 1$: Maps a narrow range of dark input values into a wider range of output values (similar to Log).
        *   If $\gamma > 1$: Maps a narrow range of bright input values into a wider range of output values (darkens the image).
    *   *Application:* Used for **Gamma Correction** in CRT monitors and modern displays to correct hardware-induced power-law distortions.

**Curves Diagram:**
```text
  Output (s)
      |   /  (Gamma < 1 / Log)  
      |  /                  
      | /  -- (Gamma = 1 / Linear)
      |/                    
      | \                   
      |  \   (Gamma > 1 / Inverse Log)
      +------------------------ Input (r)
```

---

**Q. 4. What is a Histogram? Differentiate between Histogram Equalization and Histogram Specification (Matching).**
**Introduction:**
A **Histogram** of a digital image is a discrete graphical representation showing the frequency of occurrence of each gray-level value. It provides a global description of the image's appearance.

**Main Answer:**
| Feature | Histogram Equalization (HE) | Histogram Specification (Matching) |
| :--- | :--- | :--- |
| **Objective** | Automatically produces an output image with a perfectly **uniform (flat)** histogram. | Produces an output image whose histogram matches a specific, **user-defined shape**. |
| **Process Nature** | Fully **Automatic**. The system mathematically calculates the transformation function using CDF. | **Interactive / Manual**. The user must explicitly define the target histogram shape beforehand. |
| **Flexibility** | Rigid. It always attempts to maximize global contrast indiscriminately. | Highly flexible. Useful when uniform contrast causes unnatural artifacts (e.g., washing out a face). |
| **Complexity** | Mathematically simple mapping based on Cumulative Distribution Function (CDF). | Mathematically complex. Involves equalizing the original image, equalizing the target shape, and mapping the inverse. |

**Conclusion:**
Histogram Equalization is the "one-click fix" for dark images, while Histogram Specification is the precision tool used when the aesthetic or analytical integrity of the specific gray levels must be preserved.

---

**Q. 5. What is Spatial Filtering? Explain the mechanics of spatial filtering using a $3 \times 3$ mask.**
**Introduction:**
**Spatial Filtering** is a neighborhood-based enhancement technique. Instead of changing a pixel based solely on its own value, it changes the pixel based on the values of the pixels immediately surrounding it.

**Main Answer:**
*   **The Mask:** The process uses a sub-image called a mask (or kernel/filter), which is a 2D matrix (e.g., $3 \times 3$) containing predetermined weights.
*   **The Mechanics (Convolution/Correlation):**
    1.  The center of the $3 \times 3$ mask is placed directly over the target pixel $(x,y)$ in the image.
    2.  The 9 pixel values under the mask are individually multiplied by the 9 corresponding weights in the mask.
    3.  These 9 products are summed together.
    4.  The final sum replaces the original value of the target pixel $(x,y)$ in the output image.
    5.  The mask shifts one pixel to the right, and the process repeats for the entire image.
*   **Mathematical Formula:** 
    $g(x,y) = \sum_{s=-1}^{1} \sum_{t=-1}^{1} w(s,t) \cdot f(x+s, y+t)$

**Conclusion:**
By simply changing the numbers (weights) inside the mask, spatial filtering can perform radically different tasks, from severe blurring to razor-sharp edge detection.

---

**Q. 6. Explain Image Averaging. How does averaging multiple noisy images of the same scene reduce random additive noise?**
**Introduction:**
**Image Averaging** is a powerful spatial enhancement technique used primarily in astronomy and medical imaging where identical, static scenes are captured multiple times under high-noise conditions.

**Main Answer:**
*   **The Principle:** An image $g(x,y)$ captured by a camera is a combination of the true image $f(x,y)$ and random additive noise $\eta(x,y)$.
    $g(x,y) = f(x,y) + \eta(x,y)$
*   **Noise Characteristics:** The noise $\eta(x,y)$ is assumed to be uncorrelated and has a mean value of zero (e.g., Gaussian noise). This means at any given pixel, the noise is randomly positive in one photo and negative in another.
*   **The Averaging Process:** If we capture $K$ noisy images of the exact same static scene and average them:
    $\bar{g}(x,y) = \frac{1}{K} \sum_{i=1}^{K} g_i(x,y)$
*   **The Result:** Because the true image $f(x,y)$ is identical in every frame, it remains perfectly intact. However, the random positive and negative noise values cancel each other out. Mathematically, the variance of the noise is reduced by a factor of $1/K$. As $K$ approaches infinity, the noise approaches zero.

---

**Q. 7. What is Derivative Filtering? Explain the role of the Laplacian operator in image sharpening and write down two commonly used $3 \times 3$ Laplacian masks.**
**Introduction:**
**Derivative Filtering** utilizes spatial differentiation to highlight rapid transitions in intensity (edges) while completely suppressing areas of constant intensity (backgrounds). It is the backbone of Image Sharpening.

**Main Answer:**
*   **The Laplacian Operator:** The Laplacian is an isotropic (rotation-invariant) **second-order derivative**. 
    $\nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}$
*   **Role in Sharpening:** Because it is a second-order derivative, the Laplacian excels at identifying the exact center of fine details, thin lines, and isolated points. Applying the Laplacian generates an image containing *only* the edges (often looking mostly black). To create the final sharpened image, this edge-only image is added back to the original image.
*   **Common $3 \times 3$ Laplacian Masks:**
    *   *Mask 1 (Orthogonal only):*
        $$ \begin{bmatrix} 0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0 \end{bmatrix} $$
    *   *Mask 2 (Includes diagonals):*
        $$ \begin{bmatrix} 1 & 1 & 1 \\ 1 & -8 & 1 \\ 1 & 1 & 1 \end{bmatrix} $$

---

**Q. 8. Explain the concept of High-boost Filtering. How is it different from standard High-pass filtering?**
**Introduction:**
While high-pass filtering effectively sharpens images, it completely strips away all the low-frequency background color and texture, making the image look unnatural. **High-boost filtering** resolves this.

**Main Answer:**
*   **High-Pass Filtering:**
    $Highpass = Original - Lowpass$
    The result highlights edges but removes the original visual context.
*   **High-Boost Concept:**
    High-boost filtering amplifies the high-frequency components while partially retaining the low-frequency original image. It is essentially a generalized form of unsharp masking.
    *Formula:*
    $Highboost = (A) \cdot Original - Lowpass$
    where $A \ge 1$ is the amplification factor.
*   **Rearranged for clarity:**
    $Highboost = (A - 1) \cdot Original + (Original - Lowpass)$
    $Highboost = (A - 1) \cdot Original + Highpass$
*   **Difference:** When $A = 1$, it acts exactly like a standard high-pass filter. When $A > 1$, a portion of the original image is added back to the sharp edges, resulting in a perfectly natural-looking image with greatly enhanced sharpness.

---

**Q. 9. Draw and explain the block diagram of the basic steps for Image Enhancement in the Frequency Domain.**
**Introduction:**
Frequency domain enhancement is based on the convolution theorem, which states that spatial convolution is mathematically equivalent to multiplication in the frequency domain.

**Main Answer:**
**Block Diagram:**
```text
           [ Pre-processing: Zero Padding ]
                         |
           [ Forward Transform: DFT (F(u,v)) ]
                         |
  +--- [ Multiply with Filter Function H(u,v) ] <--- [ Filter H(u,v) ]
  |                      |
  |                      v
  |              [ G(u,v) = F(u,v) * H(u,v) ]
  |                      |
  +---------- [ Inverse Transform: IDFT ]
                         |
           [ Post-processing: Extract Image ] ---> Enhanced Image g(x,y)
```

**Explanation of Steps:**
1.  **Pre-processing:** The input image $f(x,y)$ is zero-padded to prevent wraparound errors during circular convolution, and multiplied by $(-1)^{x+y}$ to center the transform.
2.  **DFT:** The image is converted into the frequency domain spectrum $F(u,v)$.
3.  **Filtering:** The spectrum $F(u,v)$ is point-by-point multiplied by a chosen filter transfer function $H(u,v)$ (e.g., a Low Pass Filter).
4.  **IDFT:** The filtered spectrum $G(u,v)$ is converted back to the spatial domain using the Inverse Discrete Fourier Transform.
5.  **Post-processing:** The real parts are extracted and un-padded to yield the final enhanced image $g(x,y)$.

---

**Q. 10. Differentiate between Ideal Low Pass Filter (ILPF) and Butterworth Low Pass Filter (BLPF) in the frequency domain. Mention the transfer function for ILPF.**
**Introduction:**
Frequency domain Low Pass Filters "cut off" high frequencies to blur an image. The way they handle this cutoff defines their mathematical properties and visual output.

**Main Answer:**
| Feature | Ideal Low Pass Filter (ILPF) | Butterworth Low Pass Filter (BLPF) |
| :--- | :--- | :--- |
| **Cutoff Shape** | Completely abrupt and sharp ("Brick-wall"). | Smooth and gradual transition. |
| **Ringing Effect** | Severe ringing effect (Gibbs phenomenon) visually degrading the image. | Ringing is significantly reduced, becoming practically invisible at lower orders. |
| **Parameter Control** | Controlled solely by Cutoff Frequency ($D_0$). | Controlled by Cutoff Frequency ($D_0$) and Filter Order ($n$). |

**Transfer Function for ILPF:**
The ILPF blocks all frequencies beyond a certain distance $D_0$ from the center.
$$ H(u,v) = \begin{cases} 1 & \text{if } D(u,v) \le D_0 \\ 0 & \text{if } D(u,v) > D_0 \end{cases} $$
*(Where $D(u,v)$ is the Euclidean distance from the origin $(u,v)$).*

---

**Q. 11. Why does the Ideal Low-Pass Filter suffer from the "Ringing Effect"? How does the Butterworth filter mitigate this?**
**Introduction:**
The "Ringing Effect" is an intolerable visual artifact in frequency domain filtering where faint, echoing ripples appear around sharp edges in the processed image.

**Main Answer:**
*   **Cause in ILPF:** The Ideal Low-Pass Filter possesses a sudden, completely abrupt, vertical "brick-wall" cutoff at the frequency $D_0$. In signal processing, the inverse Fourier transform of a perfect rectangle (sharp cutoff) is a **Sinc function**. A Sinc function looks like a wave with infinite ripples. When this spatial Sinc mask is convolved with the image, these ripples physically manifest as concentric ringing artifacts around edges.
*   **Mitigation by BLPF:** The Butterworth Low-Pass Filter avoids this by replacing the harsh, binary cutoff with a **smooth, continuous mathematical curve**. Because the frequency transition is gradual, its inverse Fourier transform does not produce aggressive Sinc-like ripples. By adjusting the "order" ($n$) of the Butterworth filter, the user controls the slope; a lower order (e.g., $n=2$) provides a perfectly smooth blur with zero perceptible ringing.

---

**Q. 12. Draw the basic block diagram of a Homomorphic Filtering system and briefly state the function of each block.**
**Introduction:**
**Homomorphic Filtering** is a unique frequency domain technique designed to tackle images suffering from severe, uneven lighting. It processes illumination and reflectance separately.

**Main Answer:**
**Block Diagram:**
```text
f(x,y) ---> [ ln ] ---> [ DFT ] ---> [ H(u,v) ] ---> [ IDFT ] ---> [ exp ] ---> g(x,y)
```

**Function of Each Block:**
1.  **Natural Log [ $\ln$ ]:** The image model $f(x,y) = i(x,y) \cdot r(x,y)$ is multiplicative. The log function converts this multiplication into addition: $\ln f = \ln i + \ln r$. This is crucial because Fourier transforms are linear and cannot cleanly separate multiplied signals.
2.  **[ DFT ]:** Transforms the logged image into the frequency domain.
3.  **Filter [ $H(u,v)$ ]:** A specialized high-frequency emphasis filter is applied. Since illumination ($i$) varies slowly (low frequencies) and reflectance ($r$) varies abruptly (high frequencies), the filter **suppresses the low frequencies** (compressing lighting) and **amplifies the high frequencies** (enhancing contrast/detail).
4.  **[ IDFT ]:** Transforms the filtered signal back to the spatial domain.
5.  **Exponential [ $\exp$ ]:** The inverse operation of the natural log. It reverses the initial mathematical shift, yielding the final, evenly lit image $g(x,y)$.

***

# GROUP C: 15-MARK QUESTIONS

### Question 1: Focus on Histogram Equalization (Numerical) (10 + 5)

**(a) Perform Histogram Equalization on an $8 \times 8$ image (3-bit, meaning 8 gray levels from 0 to 7) having the following gray-level distribution:**
*(Provided data: $r_0=0, n_0=8$; $r_1=1, n_1=10$; $r_2=2, n_2=10$; $r_3=3, n_3=16$; $r_4=4, n_4=14$; $r_5=5, n_5=4$; $r_6=6, n_6=2$; $r_7=7, n_7=0$).*
**(Show the table with PDF, CDF, multiplied values, and the new mapped pixel values, followed by the equalized histogram data). (10)**

**Main Answer:**
**Given Data:**
*   Image Size: $8 \times 8 \Rightarrow$ Total Pixels $N = 64$.
*   Bits = 3 $\Rightarrow$ Total Levels $L = 8$. Maximum Level $(L-1) = 7$.

**Calculation Table for Histogram Equalization:**

| Gray Level ($r_k$) | No. of Pixels ($n_k$) | PDF = $n_k/N$ | CDF = $\Sigma$ PDF | CDF $\times (L-1)$ | Round off ($s_k$) | New Histogram (mapped $n_k$) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **0** | 8 | 8/64 (0.125) | 8/64 | 56/64 (0.87) | **1** | $s_1$ gets 8 |
| **1** | 10 | 10/64 (0.156) | 18/64 | 126/64 (1.96)| **2** | $s_2$ gets 10 |
| **2** | 10 | 10/64 (0.156) | 28/64 | 196/64 (3.06)| **3** | $s_3$ gets 10 |
| **3** | 16 | 16/64 (0.250) | 44/64 | 308/64 (4.81)| **5** | $s_5$ gets 16 |
| **4** | 14 | 14/64 (0.218) | 58/64 | 406/64 (6.34)| **6** | $s_6$ gets 14 |
| **5** | 4 | 4/64 (0.062) | 62/64 | 434/64 (6.78)| **7** | $s_7$ gets 4 |
| **6** | 2 | 2/64 (0.031) | 64/64 | 448/64 (7.00)| **7** | $s_7$ gets 2 |
| **7** | 0 | 0/64 (0.000) | 64/64 | 448/64 (7.00)| **7** | $s_7$ gets 0 |

**Final Equalized Histogram Data:**
The old pixel counts $n_k$ are now mapped to their new gray levels $s_k$. If multiple original levels map to the same new level, their pixel counts are added together.
*   Level **0**: 0 pixels
*   Level **1**: 8 pixels
*   Level **2**: 10 pixels
*   Level **3**: 10 pixels
*   Level **4**: 0 pixels
*   Level **5**: 16 pixels
*   Level **6**: 14 pixels
*   Level **7**: (4 + 2 + 0) = 6 pixels

---

**(b) Prove theoretically that a continuous histogram equalization process yields a uniform histogram. (5)**

**Main Answer:**
**Proof:**
Let $r$ be the continuous intensity of the input image, where $r \in [0, L-1]$, with a probability density function (PDF) of $p_r(r)$.
Let the transformation function be $s = T(r)$. We want to prove that the PDF of the output image, $p_s(s)$, is completely uniform (constant).

The transformation function for Histogram Equalization is the cumulative distribution function (CDF) of $r$:
$$ s = T(r) = (L-1) \int_0^r p_r(w) dw $$

To find $p_s(s)$, we use the fundamental theorem of probability for random variables:
$$ p_s(s) = p_r(r) \left| \frac{dr}{ds} \right| $$

First, we find the derivative of the transformation function $s$ with respect to $r$. By the Fundamental Theorem of Calculus:
$$ \frac{ds}{dr} = \frac{d}{dr} \left[ (L-1) \int_0^r p_r(w) dw \right] = (L-1) p_r(r) $$

Now, substituting the inverse derivative $\frac{dr}{ds}$ back into the probability equation:
$$ p_s(s) = p_r(r) \cdot \frac{1}{(L-1) p_r(r)} $$

The $p_r(r)$ terms cancel out perfectly:
$$ p_s(s) = \frac{1}{L-1} $$

**Conclusion:**
Since $p_s(s) = \frac{1}{L-1}$ is a constant value independent of $s$, the probability density function is uniformly distributed. This mathematically proves that continuous histogram equalization always yields a perfectly flat, uniform histogram.

***

### Question 2: Focus on Spatial Filtering (Smoothing & Sharpening) (6 + 5 + 4)

**(a) Discuss spatial domain Low-pass filtering (Smoothing). How does a mean filter handle image noise, and what is its major drawback regarding image edges? (6)**

**Main Answer:**
**Low-pass Filtering (Smoothing):**
Spatial smoothing utilizes low-pass filters to blur an image and reduce high-frequency noise. The most common implementation is the **Mean (Averaging) Filter**, which replaces the value of every pixel with the mathematical average of the gray levels in its immediate neighborhood (defined by the mask).

**How it handles noise:**
Noise typically manifests as sharp, isolated, random spikes in pixel intensity. Because the mean filter averages the spiked pixel with its 8 surrounding normal pixels, the intensity of the noise spike is severely diluted and suppressed, smoothing out the grainy appearance of the image.

**Major Drawback (Edge Blurring):**
While it successfully suppresses noise, it indiscriminately suppresses *all* high-frequency components. **Edges**—the sharp, critical transitions that define object boundaries in an image—are also high-frequency components. Averaging the pixels across an edge causes the edge to widen, destroying the sharpness and resulting in a heavily blurred, out-of-focus image.

---

**(b) What are spatial High-pass filters? Explain how the Laplacian operator is used for image sharpening. Show how the sharpened image is obtained by combining the original image and the Laplacian image. (5)**

**Main Answer:**
**Spatial High-pass Filters:**
These are sharpening filters that suppress low-frequency background details and amplify high-frequency details (edges, points, and fine lines). The sum of all weights in a high-pass mask is always zero.

**The Laplacian Operator:**
The Laplacian is a linear, isotropic second-order derivative operator. It detects rapid changes in intensity perfectly, regardless of edge direction.
Applying the Laplacian mask produces an image containing *only* the grayish/black edges, stripped of all original visual context.

**Combining to obtain the Sharpened Image:**
To restore the visual context while enhancing the edges, the Laplacian edge-image must be mathematically combined with the original image.
$$ g(x,y) = f(x,y) + c \cdot \nabla^2 f(x,y) $$
*   Where $f(x,y)$ is the original image.
*   $\nabla^2 f(x,y)$ is the Laplacian edge-image.
*   $c$ is $-1$ if the center of the Laplacian mask is negative, and $+1$ if the center is positive.
Adding the edges back to the original image artificially thickens and highlights the borders, resulting in a crisp, sharp output.

---

**(c) Explain Unsharp Masking and High-boost filtering mathematically. (4)**

**Main Answer:**
**Unsharp Masking** is a classic sharpening process used in the printing industry, executed in three mathematical steps:
1.  Blur the original image to create a smoothed version: $f_{smooth}(x,y)$
2.  Subtract the smoothed image from the original to create an edge-only "mask":
    $g_{mask}(x,y) = f(x,y) - f_{smooth}(x,y)$
3.  Add the mask back to the original image to sharpen it:
    $g(x,y) = f(x,y) + k \cdot g_{mask}(x,y)$

**High-Boost Filtering:**
High-boost filtering is simply a generalized mathematical extension of Unsharp Masking controlled by the weight variable $k$.
*   If $k = 1$: The process is standard **Unsharp Masking**.
*   If $k > 1$: The process is called **High-boost Filtering**. The edges are amplified significantly more than the background, creating highly aggressive sharpening.

***

### Question 3: Focus on Frequency Domain Filtering (7 + 4 + 4)

**(a) Define Ideal, Butterworth, and Gaussian High-pass filters in the frequency domain with their respective mathematical transfer functions $H(u,v)$. (7)**

**Main Answer:**
High-pass filters block low frequencies (distance $< D_0$) and pass high frequencies (distance $\ge D_0$).
Let $D(u,v)$ be the Euclidean distance from the frequency center.

1.  **Ideal High-Pass Filter (IHPF):**
    Cuts off low frequencies completely and abruptly.
    $$ H(u,v) = \begin{cases} 0 & \text{if } D(u,v) \le D_0 \\ 1 & \text{if } D(u,v) > D_0 \end{cases} $$
2.  **Butterworth High-Pass Filter (BHPF):**
    Provides a smooth, mathematical transition curve. The slope is controlled by order $n$.
    $$ H(u,v) = \frac{1}{1 + \left( \frac{D_0}{D(u,v)} \right)^{2n}} $$
3.  **Gaussian High-Pass Filter (GHPF):**
    Based on the exponential Gaussian curve. It is the smoothest transition possible.
    $$ H(u,v) = 1 - e^{-\frac{D^2(u,v)}{2D_0^2}} $$

---

**(b) Compare the visual results (e.g., ringing effect, edge sharpness) of applying ILPF, BLPF, and GLPF on an image. (4)**

**Main Answer:**
When applied to an image to induce blurring:
*   **ILPF (Ideal):** Produces severe, distracting ripples around every edge in the image due to the massive **Ringing Effect**. It is completely useless for practical image enhancement.
*   **BLPF (Butterworth):** Produces a highly effective, natural-looking blur. Depending on the order $n$, ringing is either negligible or completely imperceptible. Edge transitions are smooth.
*   **GLPF (Gaussian):** Produces the most mathematically perfect, visually pleasing blur. It is mathematically guaranteed to exhibit **Zero Ringing Effect** because the inverse Fourier transform of a Gaussian curve is another smooth Gaussian curve.

---

**(c) Why is it necessary to perform zero-padding before applying the Discrete Fourier Transform (DFT) in frequency domain filtering? (4)**

**Main Answer:**
In the frequency domain, multiplication of two transforms corresponds to **Circular Convolution** in the spatial domain, not linear convolution. 
Because the DFT treats images as infinite, repeating, periodic grids, circular convolution causes the mathematical edges of the image to overlap and wrap around onto the opposite sides of the image. This creates severe, unnatural ghosting artifacts at the image borders known as the **Wraparound Error**.
To prevent this, we perform **Zero-padding**: If image A is $M \times N$ and mask B is $P \times Q$, we pad both with zeros to a new size $(M+P-1) \times (N+Q-1)$ before taking the DFT. This creates enough empty space to absorb the convolution overlap, perfectly simulating linear convolution.

***

### Question 4: Focus on Homomorphic Filtering & Contrast (7 + 8)

**(a) Explain Homomorphic Filtering in detail with the help of a block diagram. How does it independently control the illumination and reflectance components of an image? (7)**

**Main Answer:**
**Concept:**
Homomorphic Filtering is a frequency domain technique used to correct images suffering from extreme, uneven lighting (e.g., a face hidden in dark shadow against a bright sky). It utilizes the image model $f(x,y) = i(x,y) \cdot r(x,y)$. 

**Independent Control:**
*   **Illumination ($i$)** changes slowly across an image, meaning it sits in the **low-frequency** spectrum.
*   **Reflectance ($r$)** changes abruptly at object edges, meaning it sits in the **high-frequency** spectrum.
By converting the multiplicative model into an additive model using logarithms, the Fourier transform can separate these frequencies. A customized filter is then applied that heavily suppresses low frequencies (darkening bright skies, lightening dark shadows) while amplifying high frequencies (sharpening details).

**Block Diagram:**
```text
f(x,y) ---> [ ln ] ---> [ DFT ] ---> [ H(u,v) ] ---> [ IDFT ] ---> [ exp ] ---> g(x,y)
```
1.  $\ln$: Logarithm converts multiplication to addition: $\ln(f) = \ln(i) + \ln(r)$.
2.  **DFT**: Transforms the logged signal to frequency space.
3.  **$H(u,v)$**: The Homomorphic filter is applied. It decreases the contribution of low frequencies (illumination) and increases high frequencies (reflectance).
4.  **IDFT**: Transforms back to spatial space.
5.  **$\exp$**: The exponential function reverses the log, returning the final image.

---

**(b) Define piecewise linear transformation functions. Explain Contrast Stretching, Gray-level Slicing (with and without background), and Bit-plane Slicing with necessary diagrams. (8)**

**Main Answer:**
**Piecewise Linear Transformations:**
These are spatial domain enhancement functions composed of multiple distinct, straight-line mathematical segments, allowing different sections of the gray-level spectrum to be altered differently.

**1. Contrast Stretching:**
Expands a narrow range of intensities to the full dynamic range (e.g., $0-255$).
*(Diagram: A Z-shaped curve where input values below $r_1$ are squashed to 0, values above $r_2$ are pushed to 255, and the middle is steeply stretched).*

**2. Gray-level Slicing:**
Highlights a specific, critical range of gray levels (e.g., isolating the density of a tumor in an X-ray) while handling the rest of the image in two ways:
*   **Without Background:** The target range is set to maximum white, and everything else is forced to absolute black. (Curve looks like a square pulse).
*   **With Background:** The target range is set to maximum white, but the original background intensities are perfectly preserved. (Curve looks like a step-up over a $45^\circ$ line).

**3. Bit-plane Slicing:**
Instead of highlighting intensity ranges, it highlights the contribution of specific bits. An 8-bit image is split into 8 separate binary planes.
*   The **Higher-order planes (Plane 7 & 6)** contain the vast majority of visually significant structural data.
*   The **Lower-order planes (Plane 0 & 1)** contain mostly random noise and micro-textures.
*   *Application:* Bit-plane slicing is heavily used in Image Compression, as discarding the lowest 4 planes halves the file size without visibly destroying the image structure.

***

### Question 5: Mixed Practical & Theoretical Bag (5 + 5 + 5)

**(a) Write a short note on Image Averaging for noise reduction. If you average $K$ noisy images, by what factor is the noise variance reduced? (5)**

**Main Answer:**
**Image Averaging** relies on the statistical properties of zero-mean random noise (like sensor grain in low light). If a camera captures the exact same static scene $K$ times, the true image data remains mathematically constant across all frames, but the noise randomly fluctuates between positive and negative values.
By adding the $K$ images together and dividing by $K$, the true image aligns and preserves itself, while the random noise mathematically cancels itself out.
**Variance Reduction Factor:**
If the original noise has a variance of $\sigma^2$, the noise variance of the final averaged image is reduced to **$\frac{\sigma^2}{K}$**. The standard deviation (the visible noise) drops by $\frac{1}{\sqrt{K}}$.

---

**(b) Explain the concept of First-order derivatives (Gradient / Sobel operator) for edge enhancement. Provide the horizontal and vertical Sobel masks. (5)**

**Main Answer:**
**First-order derivatives** measure the rate of change of pixel intensity. They produce non-zero values wherever an edge exists and absolute zero in areas of constant color. The magnitude of the **Gradient** vector is used to enhance these edges, producing thick, prominent outlines around objects.

**The Sobel Operator:**
The Sobel operator is the most popular first-order gradient mask because it incorporates slight smoothing, making it robust against noise that usually ruins derivative calculations. It uses two masks, one for horizontal edges and one for vertical edges.

**Sobel Masks:**
*   Horizontal ($G_x$):
    $$ \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix} $$
*   Vertical ($G_y$):
    $$ \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix} $$

---

**(c) Contrast Frequency Domain Low-pass filtering with Frequency Domain High-pass filtering. Give one practical application for each. (5)**

**Main Answer:**
| Feature | FD Low-Pass Filtering | FD High-Pass Filtering |
| :--- | :--- | :--- |
| **Operation** | Blocks high frequencies; Passes low frequencies. | Blocks low frequencies; Passes high frequencies. |
| **Visual Effect** | Causes severe **Blurring / Smoothing**. | Causes aggressive **Sharpening / Edge Detection**. |
| **Mask Center** | High values at the center (origin), dropping to zero towards the edges. | Zero at the center (origin), rising to high values towards the edges. |
| **Noise Impact** | Destroys sharp noise spikes (noise reduction). | Amplifies random noise (major drawback). |
| **Practical Application** | Removing facial wrinkles in portrait photography or blurring satellite images to extract overall terrain regions. | Medical imaging (enhancing micro-calcifications in mammograms) or fingerprint analysis. |
