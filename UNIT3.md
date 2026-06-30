# GROUP A: 1-MARK QUESTIONS (SHORT ANSWER)

**Pixel Connectivity & Relations:**

**Q. 1. Let $p$ be a pixel at coordinate $(x, y)$. What are the coordinates of its 4-neighbors ($N_4(p)$)?**
**Main Answer:** The 4-neighbors of $p$ are its immediate vertical and horizontal neighbors, located at coordinates **$(x+1, y), (x-1, y), (x, y+1),$** and **$(x, y-1)$**.

**Q. 2. What are the diagonal neighbors ($N_D(p)$) of a pixel at $(x, y)$?**
**Main Answer:** The diagonal neighbors are located at the four corners of the pixel: **$(x+1, y+1), (x+1, y-1), (x-1, y+1),$** and **$(x-1, y-1)$**.

**Q. 3. What is the total number of pixels in the 8-neighborhood ($N_8(p)$) of a pixel?**
**Main Answer:** There are exactly **8 pixels** in the 8-neighborhood of a pixel, consisting of its 4-neighbors and 4 diagonal neighbors.

**Q. 4. What is the primary reason for introducing m-connectivity (mixed connectivity)?**
**Main Answer:** **m-connectivity** is introduced to eliminate the **multiple path connections (ambiguities)** that frequently arise when using standard 8-connectivity, ensuring single, well-defined paths along object boundaries.

**Q. 5. For a relation to be an Equivalence Relation, what three properties must it satisfy?**
**Main Answer:** It must be **Reflexive**, **Symmetric**, and **Transitive**.

**Q. 6. In image processing, what does the 'Transitive Closure' of a connectivity relation help to find?**
**Main Answer:** Transitive closure helps mathematically identify all pixels belonging to the same **connected component (region)** within an image.

**Distance Measures & Arithmetic/Logic:**

**Q. 7. Write the formula for the Euclidean distance ($D_e$) between two pixels $p(x, y)$ and $q(s, t)$.**
**Main Answer:** The Euclidean distance is: **$D_e(p,q) = \sqrt{(x-s)^2 + (y-t)^2}$**.

**Q. 8. Write the formula for the City-block distance ($D_4$) between two pixels.**
**Main Answer:** The City-block distance is: **$D_4(p,q) = |x-s| + |y-t|$**.

**Q. 9. Write the formula for the Chessboard distance ($D_8$) between two pixels.**
**Main Answer:** The Chessboard distance is: **$D_8(p,q) = \max(|x-s|, |y-t|)$**.

**Q. 10. Which arithmetic operation is widely used for motion detection or finding differences between two image frames?**
**Main Answer:** Image **Subtraction**.

**Q. 11. Which arithmetic operation is used to reduce zero-mean additive noise (like Gaussian noise)?**
**Main Answer:** Image **Addition (Averaging)**.

**Q. 12. Which logical operation is commonly used for image masking or extracting a Region of Interest (ROI)?**
**Main Answer:** The **AND** operation is used for masking.

**Transforms (Fourier, DCT, DST):**

**Q. 13. Write the mathematical formula for the Continuous 2D Fourier Transform.**
**Main Answer:** $F(u,v) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f(x,y) e^{-j2\pi(ux+vy)} dx dy$

**Q. 14. What does the magnitude of the Fourier Transform represent visually?**
**Main Answer:** The magnitude represents the **amplitude or strength** of the various spatial frequency components present in the image (indicating contrast and edges).

**Q. 15. State the Translation property of the 2D Fourier Transform.**
**Main Answer:** Shifting the spatial image $f(x-x_0, y-y_0)$ does not change the magnitude of the Fourier Transform; it only adds a **phase shift** of $e^{-j2\pi(ux_0/M + vy_0/N)}$.

**Q. 16. What is the Convolution Theorem in the frequency domain?**
**Main Answer:** The convolution of two functions in the spatial domain is mathematically equivalent to their **point-by-point multiplication** in the frequency domain.

**Q. 17. What does the acronym DCT stand for?**
**Main Answer:** **Discrete Cosine Transform**.

**Q. 18. What does the acronym DST stand for?**
**Main Answer:** **Discrete Sine Transform**.

**Q. 19. Mention one major advantage of DCT over DFT in image compression.**
**Main Answer:** DCT provides vastly superior **energy compaction**, packing most of the visual information into a very small number of low-frequency, real-valued coefficients.

**Q. 20. True or False: The 2D Discrete Fourier Transform is a separable transform.**
**Main Answer:** **True**. (It can be computed as 1D transforms along rows, followed by 1D transforms along columns).

***

# GROUP B: 5-MARK QUESTIONS

**Q. 1. Define 4-connectivity, 8-connectivity, and m-connectivity. Why is m-connectivity preferred over 8-connectivity in certain edge-linking scenarios? Give an example.**
**Introduction:**
Connectivity between pixels establishes the boundaries of objects and regions in a digital image. Let $V$ be the set of gray-level values defining adjacency (e.g., $V=\{1\}$ for binary images).

**Main Answer:**
1.  **4-Connectivity:** Two pixels $p$ and $q$ with values in $V$ are 4-connected if $q$ is in the set $N_4(p)$.
2.  **8-Connectivity:** Two pixels $p$ and $q$ with values in $V$ are 8-connected if $q$ is in the set $N_8(p)$.
3.  **m-Connectivity (Mixed):** Two pixels $p$ and $q$ with values in $V$ are m-connected if:
    *   $q$ is in $N_4(p)$, **OR**
    *   $q$ is in $N_D(p)$ (diagonal) **AND** the set $N_4(p) \cap N_4(q)$ contains no pixels whose values are from $V$.

**Why m-connectivity is preferred:**
8-connectivity often yields **multiple paths** between two pixels, creating "thick" boundaries and ambiguities in edge-tracing algorithms. M-connectivity introduces a strict rule that destroys this ambiguity, ensuring that only a single, mathematically robust 1-pixel-thick path exists between adjacent edge pixels.

**Conclusion:**
By enforcing m-connectivity, edge-detection algorithms avoid looping and branching errors, resulting in crisp, well-defined single-pixel object boundaries.

---

**Q. 2. Explain the concept of Equivalence Relation and Transitive Closure in the context of pixel connectivity (connected components).**
**Introduction:**
To mathematically group pixels into meaningful "objects," image processing relies on the set-theory concepts of equivalence relations and transitive closures.

**Main Answer:**
*   **Equivalence Relation:** For connectivity to form a valid grouping, the adjacency relation $R$ between pixels must satisfy three rules:
    1.  **Reflexive:** $p R p$ (A pixel is connected to itself).
    2.  **Symmetric:** If $p R q$, then $q R p$ (If $p$ connects to $q$, $q$ connects to $p$).
    3.  **Transitive:** If $p R q$ and $q R z$, then $p R z$ (If $p$ connects to $q$, and $q$ connects to $z$, then $p$ is logically connected to $z$).
*   **Transitive Closure:** While a pixel $p$ might only be *adjacent* to its immediate neighbor $q$, the transitive property allows us to trace a path through a chain of adjacent pixels ($p \to q \to r \to s$). The set of all pixels that can be reached from $p$ through such chains forms the **Transitive Closure**.

**Conclusion:**
In image processing, the transitive closure of the adjacency relation is exactly what defines a **Connected Component** (a distinct object or region) in an image.

---

**Q. 3. Discuss the three primary distance measures: Euclidean distance, City-block ($D_4$) distance, and Chessboard ($D_8$) distance. Draw the contour (shape of points at a constant distance) for $D_4$ and $D_8$.**
**Introduction:**
A distance measure (metric) quantifies the spatial separation between two pixels $p(x,y)$ and $q(s,t)$.

**Main Answer:**
1.  **Euclidean Distance ($D_e$):** The straight-line "crow-flies" distance.
    $D_e(p,q) = \sqrt{(x-s)^2 + (y-t)^2}$.
    *Contour Shape:* A perfect **Circle**.
2.  **City-block Distance ($D_4$):** Calculates distance assuming movement is restricted strictly to horizontal and vertical steps (like a grid of city streets).
    $D_4(p,q) = |x-s| + |y-t|$.
    *Contour Shape:* A **Diamond / Rhombus**.
3.  **Chessboard Distance ($D_8$):** Calculates distance assuming movement can happen horizontally, vertically, and diagonally with equal cost (like a King on a chessboard).
    $D_8(p,q) = \max(|x-s|, |y-t|)$.
    *Contour Shape:* A **Square**.

**Diagram (Contours of distance 2 from center):**
```text
      D4 (Diamond)             D8 (Square)
        2                      2 2 2 2 2
      2 1 2                    2 1 1 1 2
    2 1 0 1 2                  2 1 0 1 2
      2 1 2                    2 1 1 1 2
        2                      2 2 2 2 2
```

---

**Q. 4. Explain how image subtraction is used in medical imaging (like Digital Subtraction Angiography) and security systems (motion detection).**
**Introduction:**
Image subtraction is a pixel-by-pixel arithmetic operation: $g(x,y) = f(x,y) - h(x,y)$. It is highly effective for isolating changes or dynamic differences between two images.

**Main Answer:**
*   **Digital Subtraction Angiography (DSA) in Medicine:**
    1.  An X-ray image of the patient's vascular system is taken *before* injecting a contrast dye (this is the "Mask" image).
    2.  The contrast dye is injected, and a second "Live" X-ray image is captured.
    3.  By subtracting the Mask image from the Live image, the static background (bones, tissue) perfectly cancels out (becomes zero/black).
    4.  The output image strictly displays the blood vessels highlighted by the dye, allowing doctors to detect blockages.
*   **Security Systems (Motion Detection):**
    A security camera holds a reference frame of the empty room (Background). It continually subtracts the incoming live video frame from this background. If the room is empty, the subtraction yields zero (black). If an intruder walks in, the pixel subtraction yields a non-zero value at the intruder's location, instantly triggering the motion alarm.

---

**Q. 5. Explain the application of logical operations (AND, OR, NOT) in image processing with the concept of bit-planes and masking.**
**Introduction:**
Logical operations function strictly on binary images (0s and 1s) and are applied pixel-by-pixel to extract specific structural regions.

**Main Answer:**
1.  **NOT (Inversion):** Inverts a binary image (0 becomes 1, 1 becomes 0), effectively creating a negative image.
2.  **AND (Masking / ROI Extraction):** Used to extract a specific Region of Interest (ROI). 
    *   An image is ANDed with a "Mask Image" (containing 1s in the ROI and 0s elsewhere). 
    *   The resulting image retains the original pixel values inside the ROI, while turning everything outside the ROI to absolute black (0).
3.  **OR (Overlaying):** Used to superimpose or blend two binary structures together.
4.  **Bit-plane Slicing:** A grayscale image (8-bit) is composed of 8 binary bit-planes. The MSB (Bit 7) contains the primary visual structure. We can use the bitwise AND operator with the value `10000000` (128) to mathematically extract only the 7th bit-plane, completely discarding the lower-order noise planes.

---

**Q. 6. Define the 2D Discrete Fourier Transform (DFT) and its Inverse (IDFT). Explain the physical significance of the DC component $F(0,0)$.**
**Introduction:**
The Discrete Fourier Transform (DFT) transforms a spatial domain image into its frequency domain representation, decomposing the image into a sum of 2D sine and cosine waves.

**Main Answer:**
*   **2D DFT Formula:** For an image $f(x,y)$ of size $M \times N$:
    $$F(u,v) = \frac{1}{MN} \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x,y) e^{-j2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)}$$
*   **2D IDFT Formula:**
    $$f(x,y) = \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} F(u,v) e^{j2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)}$$
*   **Physical Significance of the DC Component $F(0,0)$:**
    If we substitute $u=0$ and $v=0$ into the DFT equation, the exponential term becomes $e^0 = 1$. The equation collapses to:
    $$F(0,0) = \frac{1}{MN} \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x,y)$$
    This mathematically proves that the DC component $F(0,0)$ represents the **average gray-level intensity** of the entire image.

---

**Q. 7. State and mathematically prove the Separability property of the 2D Fourier Transform. Why is this property computationally important?**
**Introduction:**
The separability property allows a complex 2D mathematical operation to be broken down into two simpler 1D operations, drastically reducing processing time.

**Main Answer:**
*   **Statement:** The 2D DFT is separable, meaning it can be computed by calculating the 1D DFT along the rows of the image, followed by the 1D DFT along the columns of the intermediate result.
*   **Proof:** 
    The 2D DFT equation is:
    $$F(u,v) = \frac{1}{MN} \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x,y) e^{-j2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)}$$
    We can rewrite the exponential term: $e^{-j2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)} = e^{-j2\pi \frac{ux}{M}} \cdot e^{-j2\pi \frac{vy}{N}}$.
    Rearranging the sums:
    $$F(u,v) = \frac{1}{M} \sum_{x=0}^{M-1} \left[ \frac{1}{N} \sum_{y=0}^{N-1} f(x,y) e^{-j2\pi \frac{vy}{N}} \right] e^{-j2\pi \frac{ux}{M}}$$
    The bracketed term is simply the 1D DFT of the rows $F(x,v)$. The outer sum is the 1D DFT of the columns $F(u,v)$. (Proved).
*   **Computational Importance:** 
    Computing a 2D DFT directly takes $O(N^4)$ operations. Using the separability property with the 1D Fast Fourier Transform (FFT) reduces the complexity to **$O(N^2 \log_2 N)$**, making real-time image processing possible.

---

**Q. 8. State and mathematically prove the Translation property (Shift theorem) of the 2D Fourier Transform.**
**Introduction:**
The translation property defines the relationship between shifting an image physically in space and how its frequency spectrum reacts.

**Main Answer:**
*   **Statement:** A spatial shift of an image $f(x,y)$ to $f(x-x_0, y-y_0)$ does not alter the magnitude of the Fourier Transform; it only induces a phase shift in the frequency domain.
    $$ f(x-x_0, y-y_0) \iff F(u,v) e^{-j2\pi \left(\frac{ux_0}{M} + \frac{vy_0}{N}\right)} $$
*   **Proof:**
    Let $g(x,y) = f(x-x_0, y-y_0)$. Its DFT is:
    $$ G(u,v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x-x_0, y-y_0) e^{-j2\pi \left(\frac{ux}{M} + \frac{vy}{N}\right)} $$
    Substitute variables: Let $m = x - x_0$ and $n = y - y_0$. Then $x = m + x_0$ and $y = n + y_0$.
    $$ G(u,v) = \sum_m \sum_n f(m,n) e^{-j2\pi \left(\frac{u(m+x_0)}{M} + \frac{v(n+y_0)}{N}\right)} $$
    $$ G(u,v) = \left[ \sum_m \sum_n f(m,n) e^{-j2\pi \left(\frac{um}{M} + \frac{vn}{N}\right)} \right] \cdot e^{-j2\pi \left(\frac{ux_0}{M} + \frac{vy_0}{N}\right)} $$
    Since the bracketed term is exactly $F(u,v)$:
    $$ G(u,v) = F(u,v) e^{-j2\pi \left(\frac{ux_0}{M} + \frac{vy_0}{N}\right)} $$ (Proved).

---

**Q. 9. What is the Discrete Cosine Transform (DCT)? Briefly explain the concept of "Energy Compaction" and why DCT is the standard for JPEG compression.**
**Introduction:**
The Discrete Cosine Transform (DCT) decomposes an image into a sum of oscillating cosine functions of different frequencies, completely ignoring sine terms.

**Main Answer:**
*   **Concept:** DCT produces entirely real-valued coefficients (no imaginary parts), which makes it highly efficient for storage.
*   **Energy Compaction:** This is a phenomenon where the vast majority of the visual "energy" (the structural data) of the image is pushed into the **upper-left corner** of the DCT matrix (the low-frequency coefficients). The high-frequency coefficients quickly approach zero.
*   **Why it is standard for JPEG:** Because of its superior energy compaction, JPEG algorithms can safely discard (quantize to zero) over 80% of the high-frequency DCT coefficients without the human eye noticing any structural loss in the image. This yields massive file compression ratios.

---

**Q. 10. Briefly differentiate between the Discrete Fourier Transform (DFT), Discrete Cosine Transform (DCT), and Discrete Sine Transform (DST).**
**Introduction:**
While all three transforms move image data from the spatial domain to the frequency domain, their underlying basis functions and handling of image boundaries differ drastically.

**Main Answer:**
| Feature | DFT | DCT | DST |
| :--- | :--- | :--- | :--- |
| **Basis Functions** | Complex Exponentials (Sines & Cosines). | Only Cosines (Real numbers). | Only Sines (Real numbers). |
| **Image Extension** | Assumes **Periodic** extension (causes artificial sharp jumps at boundaries). | Assumes **Even/Symmetric** extension (smooth boundaries). | Assumes **Odd/Antisymmetric** extension. |
| **Energy Compaction** | Poor. Energy is spread out. | **Excellent**. Energy is tightly packed. | Poor for standard images. |
| **Primary Use Case** | Signal analysis, spatial filtering (convolution). | Image/Video Compression (JPEG, MPEG). | Solving partial differential equations. |

**Conclusion:**
DCT is strictly preferred in multimedia storage due to its smooth boundary assumptions and real-number output, avoiding the visual "blocking artifacts" caused by DFT.

***

# GROUP C: 15-MARK QUESTIONS

### Question 1: Focus on Connectivity and Distance Measures (6 + 5 + 4)

**(a) Consider an image subset $V = \{1\}$. Differentiate between 4-path, 8-path, and m-path between two pixels $p$ and $q$. Explain how m-connectivity resolves the ambiguity (multiple paths) of 8-connectivity. (6)**

**Main Answer:**
A path from pixel $p$ to pixel $q$ is a sequence of distinct pixels where adjacent pixels satisfy a specific connectivity rule. Let $V = \{1\}$ represent the object pixels.
1.  **4-path:** A path where every adjacent pixel pair $(p_i, p_{i+1})$ is 4-connected (shares an edge).
2.  **8-path:** A path where every adjacent pixel pair is 8-connected (shares an edge or a corner).
3.  **m-path:** A path where every adjacent pixel pair is m-connected.

**Ambiguity of 8-connectivity:**
Consider a $2 \times 2$ block of pixels all valued at $1$:
```text
  1(p)  1(r)
  1(s)  1(q)
```
Using 8-connectivity, to get from $p$ to $q$, there are multiple valid paths:
*   Path 1: $p \to q$ (Directly diagonal)
*   Path 2: $p \to r \to q$
*   Path 3: $p \to s \to q$
This creates "thick" ambiguous boundaries which confuse edge-tracing algorithms.

**How m-connectivity resolves this:**
M-connectivity states that a diagonal connection is ONLY allowed if the common 4-neighborhood contains NO object pixels (pixels from $V$).
In the block above, $p$ and $q$ are diagonal. Their common 4-neighbors are $r$ and $s$. Since $r$ and $s$ have values of $1$ (which are in $V$), the diagonal connection $p \to q$ is **strictly forbidden**. The path *must* travel through $r$ or $s$. This eliminates the overlapping diagonal cross-paths, reducing the boundary to a single, mathematically pure 1-pixel-thick line.

---

**(b) Define the three conditions a metric $D$ must satisfy to be considered a valid Distance Measure (Positivity, Symmetry, Triangle Inequality). Check if City-block distance ($D_4$) satisfies the triangle inequality. (5)**

**Main Answer:**
For a function $D(p,q)$ to be a valid distance metric, it must satisfy:
1.  **Positivity:** $D(p,q) \ge 0$, and $D(p,q) = 0$ if and only if $p = q$.
2.  **Symmetry:** $D(p,q) = D(q,p)$. (Distance from A to B is the same as B to A).
3.  **Triangle Inequality:** $D(p,z) \le D(p,q) + D(q,z)$. (The direct path is always the shortest).

**Checking City-block ($D_4$) for Triangle Inequality:**
Given $p(x_1, y_1)$, $q(x_2, y_2)$, and $z(x_3, y_3)$.
We must show: $D_4(p,z) \le D_4(p,q) + D_4(q,z)$.
*LHS:* $D_4(p,z) = |x_1 - x_3| + |y_1 - y_3|$
*RHS:* $D_4(p,q) + D_4(q,z) = |x_1 - x_2| + |y_1 - y_2| + |x_2 - x_3| + |y_2 - y_3|$

Using the mathematical absolute value triangle inequality property ($|a - c| \le |a - b| + |b - c|$):
$|x_1 - x_3| \le |x_1 - x_2| + |x_2 - x_3|$
$|y_1 - y_3| \le |y_1 - y_2| + |y_2 - y_3|$

Adding these two valid inequalities together:
$|x_1 - x_3| + |y_1 - y_3| \le (|x_1 - x_2| + |x_2 - x_3|) + (|y_1 - y_2| + |y_2 - y_3|)$
$D_4(p,z) \le D_4(p,q) + D_4(q,z)$

**Conclusion:** Yes, the City-block distance $D_4$ perfectly satisfies the triangle inequality and is a mathematically valid metric.

---

**(c) Calculate the $D_4$ (City-block) and $D_8$ (Chessboard) distances between the pixels $P(2, 3)$ and $Q(5, 7)$. Show the formulas used. (4)**

**Main Answer:**
Given coordinates: $P(x_1, y_1) = P(2, 3)$ and $Q(x_2, y_2) = Q(5, 7)$.

**1. City-block Distance ($D_4$):**
*   **Formula:** $D_4(P,Q) = |x_1 - x_2| + |y_1 - y_2|$
*   **Calculation:** 
    $D_4(P,Q) = |2 - 5| + |3 - 7|$
    $D_4(P,Q) = |-3| + |-4|$
    $D_4(P,Q) = 3 + 4 = \mathbf{7}$

**2. Chessboard Distance ($D_8$):**
*   **Formula:** $D_8(P,Q) = \max(|x_1 - x_2|, |y_1 - y_2|)$
*   **Calculation:**
    $D_8(P,Q) = \max(|2 - 5|, |3 - 7|)$
    $D_8(P,Q) = \max(|-3|, |-4|)$
    $D_8(P,Q) = \max(3, 4) = \mathbf{4}$

***

### Question 2: Focus on Fourier Transform Properties (Proofs) (6 + 5 + 4)

**(a) State and prove the 2D Convolution Theorem. Explain why filtering is computationally faster in the frequency domain using this theorem. (6)**

**Main Answer:**
**Statement:** The Convolution Theorem states that spatial convolution of two functions corresponds to point-wise multiplication of their Fourier transforms in the frequency domain, and vice versa.
$$ f(x,y) \ast h(x,y) \iff F(u,v) \cdot H(u,v) $$

**Proof:**
By definition, the 2D spatial convolution is:
$$ g(x,y) = \iint f(\alpha, \beta) h(x-\alpha, y-\beta) d\alpha d\beta $$
Taking the Fourier transform of $g(x,y)$:
$$ G(u,v) = \iint \left[ \iint f(\alpha, \beta) h(x-\alpha, y-\beta) d\alpha d\beta \right] e^{-j2\pi(ux+vy)} dx dy $$
Rearranging integrals to isolate $x,y$:
$$ G(u,v) = \iint f(\alpha, \beta) \left[ \iint h(x-\alpha, y-\beta) e^{-j2\pi(ux+vy)} dx dy \right] d\alpha d\beta $$
Substitute variables: $m = x-\alpha, n = y-\beta$. Thus $x = m+\alpha, y = n+\beta$:
$$ G(u,v) = \iint f(\alpha, \beta) \left[ \iint h(m, n) e^{-j2\pi(u(m+\alpha) + v(n+\beta))} dm dn \right] d\alpha d\beta $$
$$ G(u,v) = \iint f(\alpha, \beta) e^{-j2\pi(u\alpha + v\beta)} d\alpha d\beta \cdot \iint h(m, n) e^{-j2\pi(um + vn)} dm dn $$
The first term is the FT of $f(x,y)$ and the second is the FT of $h(x,y)$.
Therefore, **$G(u,v) = F(u,v) \cdot H(u,v)$**. (Proved).

**Computational Speedup:**
Spatial convolution involves sliding a mask over an image, requiring $O(N^2 M^2)$ operations. By using the Fast Fourier Transform (FFT) algorithm, converting to the frequency domain requires $O(N \log N)$ operations. Point-wise multiplication is instantaneous, making frequency domain filtering exponentially faster for large filter masks.

---

**(b) State and prove the Rotation property of the 2D Continuous Fourier Transform (using polar coordinates). (5)**

**Main Answer:**
**Statement:** Rotating the spatial image $f(x,y)$ by an angle $\theta_0$ rotates its Fourier transform $F(u,v)$ by the exact same angle $\theta_0$ in the frequency plane.

**Proof:**
Using polar coordinates for spatial domain: $x = r \cos\theta, y = r \sin\theta$.
Using polar coordinates for frequency domain: $u = \omega \cos\phi, v = \omega \sin\phi$.
Substitute into the Fourier Transform formula:
$$ F(u,v) = \iint f(x,y) e^{-j2\pi(ux+vy)} dx dy $$
The exponent term $(ux + vy)$ becomes:
$ux + vy = \omega r \cos\phi \cos\theta + \omega r \sin\phi \sin\theta = \omega r \cos(\theta - \phi)$
Therefore, the transform in polar form is:
$$ F(\omega, \phi) = \iint f(r, \theta) e^{-j2\pi \omega r \cos(\theta - \phi)} r dr d\theta $$
Now, rotate the image $f(r, \theta)$ by an angle $\theta_0$, so it becomes $f(r, \theta - \theta_0)$. Its transform $F_{rot}$ is:
$$ F_{rot}(\omega, \phi) = \iint f(r, \theta - \theta_0) e^{-j2\pi \omega r \cos(\theta - \phi)} r dr d\theta $$
Substitute $\alpha = \theta - \theta_0 \implies d\alpha = d\theta$. The angle becomes $\theta = \alpha + \theta_0$:
$$ F_{rot}(\omega, \phi) = \iint f(r, \alpha) e^{-j2\pi \omega r \cos(\alpha + \theta_0 - \phi)} r dr d\alpha $$
$$ F_{rot}(\omega, \phi) = \iint f(r, \alpha) e^{-j2\pi \omega r \cos(\alpha - (\phi - \theta_0))} r dr d\alpha $$
This matches the exact original Fourier formula, but the frequency angle is now shifted by $\theta_0$.
Thus, **$F_{rot}(\omega, \phi) = F(\omega, \phi - \theta_0)$**. (Proved).

---

**(c) Explain the Scaling property of the 2D Fourier Transform. What happens to the frequency spectrum if the spatial image is compressed? (4)**

**Main Answer:**
**Scaling Property:**
$$ f(ax, by) \iff \frac{1}{|ab|} F\left(\frac{u}{a}, \frac{v}{b}\right) $$
This mathematical property demonstrates an inverse relationship between the spatial domain and the frequency domain.

**Effect of Spatial Compression:**
If the spatial image is compressed (shrunk), the scaling factors $a$ and $b$ are greater than $1$. In the frequency domain formula, $u$ and $v$ are divided by $a$ and $b$. Mathematically, this causes the frequency spectrum $F(u,v)$ to **expand (stretch out)**. 
Physically, shrinking an image squeezes the pixels closer together, generating sharper transitions. Sharp transitions require much higher frequencies to represent them, which pushes the energy of the frequency spectrum outward into the higher frequency bands.

***

### Question 3: Focus on Transforms (DFT vs DCT) (7 + 4 + 4)

**(a) Write the equations for the 2D Discrete Cosine Transform (DCT) and its inverse. Explain the basis functions of the DCT. (7)**

**Main Answer:**
**2D Forward DCT Equation:**
For an $N \times N$ image $f(x,y)$:
$$ C(u,v) = \alpha(u)\alpha(v) \sum_{x=0}^{N-1} \sum_{y=0}^{N-1} f(x,y) \cos\left[ \frac{(2x+1)u\pi}{2N} \right] \cos\left[ \frac{(2y+1)v\pi}{2N} \right] $$
Where $\alpha(w) = \sqrt{1/N}$ for $w=0$, and $\alpha(w) = \sqrt{2/N}$ for $w \ge 1$.

**2D Inverse DCT Equation (IDCT):**
$$ f(x,y) = \sum_{u=0}^{N-1} \sum_{v=0}^{N-1} \alpha(u)\alpha(v) C(u,v) \cos\left[ \frac{(2x+1)u\pi}{2N} \right] \cos\left[ \frac{(2y+1)v\pi}{2N} \right] $$

**Basis Functions:**
Unlike the Fourier Transform which uses complex exponentials, the basis functions of the DCT are strictly **real-valued oscillating cosine waves** of varying frequencies. By multiplying the raw image pixels with these different cosine frequencies and summing the result, the DCT evaluates how much of that specific frequency is present in the image block.

---

**(b) Compare DCT with DFT. Why does DCT yield better energy compaction and less "blocking artifact" at the boundaries than DFT? (4)**

**Main Answer:**
*   **The Periodic Assumption of DFT:** The DFT implicitly assumes that the image repeats infinitely in all directions. If the right edge of an image is black and the left edge is white, placing them side-by-side creates a violent, artificial "jump" in intensity. The DFT wastes massive amounts of high-frequency energy trying to model this fake, sharp boundary jump.
*   **The Symmetric Assumption of DCT:** The DCT avoids this by implicitly assuming that the image is **mirrored (evenly extended)** at its boundaries. A black right edge folds over into another black right edge. The boundary transition is mathematically smooth.
*   **Result:** Because the DCT creates smooth, continuous boundaries, it generates almost zero artificial high-frequency artifacts. This allows it to pack 99% of the real visual energy into the very first few low-frequency coefficients (Superior Energy Compaction), entirely eliminating the "blocking artifacts" that plague DFT compression.

---

**(c) Write the mathematical formula for the 2D Discrete Sine Transform (DST). Mention one scenario where DST might be used. (4)**

**Main Answer:**
**2D Forward DST Equation:**
For an $N \times N$ matrix:
$$ S(u,v) = \frac{2}{N+1} \sum_{x=0}^{N-1} \sum_{y=0}^{N-1} f(x,y) \sin\left[ \frac{(x+1)(u+1)\pi}{N+1} \right] \sin\left[ \frac{(y+1)(v+1)\pi}{N+1} \right] $$

**Use Scenario:**
While useless for standard JPEG compression (because it assumes the image boundaries drop to absolute zero, creating massive artifacts), the DST is heavily used in **solving partial differential equations (PDEs)**, physical boundary value problems, and certain types of advanced interpolation algorithms where odd/anti-symmetric conditions are strictly required.

***

### Question 4: Focus on Arithmetic/Logic and Pixel Relations (6 + 5 + 4)

**(a) Explain how Equivalence Relations (Reflexive, Symmetric, Transitive) are used to label connected components in a binary image. Explain the role of Transitive Closure in this process. (6)**

**Main Answer:**
**Connected Component Labeling** is an algorithm that scans an image and assigns a unique ID to each distinct object. It heavily relies on set-theory relations.

1.  **The Equivalence Relation:** We define a relation $R$ where $p R q$ means "pixel $p$ is directly adjacent to pixel $q$ and both are object pixels." For this to form a valid object, $R$ must be:
    *   *Reflexive:* $p R p$ (A pixel belongs to its own object).
    *   *Symmetric:* $p R q \implies q R p$ (Adjacency goes both ways).
    *   *Transitive:* $p R q$ and $q R z \implies p R z$.
2.  **Role of Transitive Closure:** In a real image, a pixel on the far left of a car is not *directly adjacent* to a pixel on the far right. However, through the Transitive property, the algorithm traces an unbroken path of intermediate adjacent pixels from the left side to the right side. The set of all possible pixels that can be reached from a starting pixel $p$ using this chain logic is the **Transitive Closure**. 
3.  **Result:** The algorithm isolates this closed set, designates it as an equivalence class, and labels the entire set as "Object 1".

---

**(b) Discuss Image Averaging for noise reduction. Mathematically prove that if we average $K$ noisy images, the variance of the additive Gaussian noise decreases by a factor of $K$. (5)**

**Main Answer:**
**Concept:**
Image averaging is used in astronomy and medicine. If a static scene is captured $K$ times, the true image $f(x,y)$ remains constant, but the additive Gaussian noise $\eta_i(x,y)$ varies randomly (mean $= 0$, variance $= \sigma^2$).
The noisy image is $g_i(x,y) = f(x,y) + \eta_i(x,y)$.

**Mathematical Proof:**
The averaged image $\bar{g}(x,y)$ is calculated as:
$$ \bar{g}(x,y) = \frac{1}{K} \sum_{i=1}^K g_i(x,y) $$
Substitute the noisy image equation:
$$ \bar{g}(x,y) = \frac{1}{K} \sum_{i=1}^K [f(x,y) + \eta_i(x,y)] $$
Since $f(x,y)$ is a constant across all $K$ images, it pulls out of the sum:
$$ \bar{g}(x,y) = f(x,y) + \frac{1}{K} \sum_{i=1}^K \eta_i(x,y) $$
Now, calculate the variance of the averaged noise term. Since the noise in each image is uncorrelated, the variance of a sum is the sum of the variances:
$$ Var\left[ \frac{1}{K} \sum \eta_i \right] = \frac{1}{K^2} \sum_{i=1}^K Var[\eta_i] $$
$$ Var_{new} = \frac{1}{K^2} (K \cdot \sigma^2) = \frac{\sigma^2}{K} $$
**Conclusion:** (Proved). The variance (noise power) drops by a factor of $K$. As $K \to \infty$, the noise approaches 0, leaving a perfectly clear image.

---

**(c) Explain Image Multiplication/Division. How is it used for shading correction (sensor non-uniformity correction)? (4)**

**Main Answer:**
*   **Image Multiplication:** Pixels from image A are multiplied by corresponding pixels in image B. It is mostly used for **Masking** (multiplying an image by a binary 0/1 mask to blank out the background).
*   **Image Division (Shading Correction):** Sensors often suffer from uneven sensitivity, or a scene might have uneven lighting (vignetting), creating a shading pattern that degrades the image.
*   **How it works:**
    1.  A photo of a perfectly flat, uniform white surface is taken under the same lighting conditions. This captures the pure error pattern (Shading Mask).
    2.  The actual degraded image is mathematically **Divided** pixel-by-pixel by the Shading Mask.
    $$ Image_{Corrected}(x,y) = \frac{Image_{Degraded}(x,y)}{Mask_{Shading}(x,y)} $$
    3.  This division perfectly cancels out the uneven lighting multiplier, restoring uniform illumination to the final image.

***

### Question 5: Mixed Mathematical Preliminaries (5 + 5 + 5)

**(a) Given a 2D image $f(x,y)$, prove that multiplying the image by $(-1)^{x+y}$ centers the 2D Fourier Transform at the origin of the frequency plane $(M/2, N/2)$. (5)**

**Main Answer:**
**Proof:**
This proof relies on the Fourier Translation Property (Shift Theorem), which states:
$$ f(x,y) e^{j2\pi \left(\frac{u_0 x}{M} + \frac{v_0 y}{N}\right)} \iff F(u - u_0, v - v_0) $$
We want to shift the origin of the frequency domain to the exact mathematical center of an $M \times N$ matrix. Therefore, we set $u_0 = M/2$ and $v_0 = N/2$.
Substitute these values into the exponential term:
$$ e^{j2\pi \left(\frac{(M/2)x}{M} + \frac{(N/2)y}{N}\right)} $$
Cancel out $M$ and $N$:
$$ = e^{j2\pi \left(\frac{x}{2} + \frac{y}{2}\right)} $$
$$ = e^{j\pi (x+y)} $$
Using Euler's formula identity, $e^{j\pi} = -1$.
Therefore:
$$ e^{j\pi (x+y)} = (e^{j\pi})^{(x+y)} = (-1)^{x+y} $$
Substituting this back into the Shift Theorem equation:
$$ f(x,y) (-1)^{x+y} \iff F\left(u - \frac{M}{2}, v - \frac{N}{2}\right) $$
**Conclusion:** (Proved). Pre-multiplying the spatial image by $(-1)^{x+y}$ perfectly shifts the zero-frequency (DC) component to the absolute center of the Fourier spectrum.

---

**(b) What are the Periodicity and Conjugate Symmetry properties of the 2D DFT? Explain their significance in storing frequency domain data. (5)**

**Main Answer:**
1.  **Periodicity:** The 2D DFT mathematically assumes that the frequency spectrum repeats infinitely in both the $u$ and $v$ directions with periods $M$ and $N$.
    $$ F(u,v) = F(u+M, v) = F(u, v+N) = F(u+M, v+N) $$
2.  **Conjugate Symmetry:** If the input spatial image $f(x,y)$ consists purely of real numbers (which all digital photos do), its Fourier transform exhibits conjugate symmetry around the origin.
    $$ F(u,v) = F^*(-u, -v) $$
    (Where $*$ denotes the complex conjugate: if $F(u,v) = a+jb$, then $F(-u,-v) = a-jb$. Their magnitudes are identical).

**Significance in Data Storage:**
Because $F(u,v)$ is a perfect mirror image of $F(-u,-v)$ in magnitude, the left half of the frequency spectrum contains the exact same visual information as the right half. Therefore, computer systems **only need to compute and store half** of the DFT matrix, cutting memory requirements and computational overhead by exactly 50%.

---

**(c) A digital image has a uniform background. Using logical operations (AND, OR), explain how you would insert a new object into this background using an object mask and a background mask. (5)**

**Main Answer:**
To seamlessly composite a new object into an existing background, we utilize Boolean logic applied pixel-by-pixel.
Let:
*   $B$ = The background image.
*   $O$ = The new object image.
*   $M$ = The object mask (a binary image where the object silhouette is $1$ (White) and the rest is $0$ (Black)).
*   $\text{NOT } M$ = The background mask (The exact inverse: object silhouette is $0$, background is $1$).

**The Process:**
1.  **Cut a hole in the background:** Compute `(B AND (NOT M))`. 
    Since the mask has $0$s where the object belongs, the AND operation turns those background pixels to absolute black, leaving a perfectly shaped "hole" for the new object.
2.  **Extract the object:** Compute `(O AND M)`.
    Since the mask has $1$s only on the object, the AND operation strips away the original background of the object image, leaving it floating in blackness.
3.  **Composite them together:** Compute the final image using `OR`.
    $$ \text{Result} = (B \text{ AND } (\text{NOT } M)) \text{ OR } (O \text{ AND } M) $$
    The OR operation seamlessly superimposes the extracted object directly into the black hole carved into the background.
