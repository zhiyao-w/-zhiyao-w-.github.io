# Final Project 1: Image Quilting
Zhiyao Wang

In this project, I implement the image quilting algorithm for texture synthesis and transfer, described in this SIGGRAPH 2001 paper by Efros and Freeman.

---

## 1. Randomly Sampled Texture

I implement the quilt_random function that randomly samples square patches of size patch_size from a sample in order to create an output image of size out_size. Start from the upper-left corner, and tile samples until the image are full.

**Parameters:**
- Patch size: 30
- Output size: 400x400

**Results:**
<p align="center">
  <img src="proj1_result/quilt_random.png" alt="quilt_random" width="30%" />
  <img src="proj1_result/text_random.png" alt="quilt_random" width="30%" />
  <img src="proj1_result/texture_random.png" alt="quilt_random" width="30%" />
</p>

## 2. Overlapping Patches

This method start by sampling a random patch for the upper-left corner. Then sample new patches to overlap with existing ones by choosing patches that have the lowest SSD cost for the overlapping regions of the patches. If tol=1, the lowest cost will always be chosen. If tol=3, one of the three lowest cost patches will be chosen.

**Parameters:**
- Patch size: 40
- Overlap size: 14
- Tolerance: 3

**Results:**
<p align="center">
  <img src="proj1_result/quilt_simple.png" alt="quilt_simple" width="30%" />
  <img src="proj1_result/text_simple.png" alt="quilt_simple" width="30%" />
  <img src="proj1_result/texture_simple.png" alt="quilt_simple" width="30%" />
</p>
The results show significant improvement over random sampling, with better continuity between patches.

## 3. Seam Finding

Next, further refines the texture synthesis by incorporate seam finding to remove edge artifacts from the overlapping patches based on section 2.1 of the paper. I find the seam by finding the min-cost contiguous path from the left to right side of the patch and create the function quilt_cut that incorporates the seam finding.

**Parameters:**
- Patch size: 40
- Overlap size: 14
- Tolerance: 3

**Results:**
<p align="center">
  <img src="proj1_result/quilt_cut.png" alt="quilt_cut" width="30%" />
  <img src="proj1_result/text_cut.png" alt="quilt_cut" width="30%" />
  <img src="proj1_result/texture_cut.png" alt="quilt_cut" width="30%" />
</p>
The seam finding approach effectively eliminates visible patch boundaries while preserving texture patterns.

## 4. Texture Transfer

I use a guidance image to do texture transferring. I modify the cost function to take a weighted sum using a parameter alpha. The weighted cost is calculated as alpha times the block overlap matching error plus (1 - alpha) times the squared error between the correspondence map pixels within the source texture block and those at the current target image position.

**Parameters:**
- Patch size: 25
- Overlap: 11
- Tolerance: 3
- Alpha: 0.5

**Results:**

sample 1:
<p align="center">
  <img src="proj1_result/sample1.png" alt="sample" width="30%" />
  <img src="proj1_result/guidance1.png" alt="guidance" width="30%" />
  <img src="proj1_result/texture_transfer1.png" alt="texture_transfer" width="30%" />
</p>
sample 2:
<p align="center">
  <img src="proj1_result/sample2.png" alt="sample" width="25%" />
  <img src="proj1_result/guidance1.png" alt="guidance" width="30%" />
  <img src="proj1_result/texture_transfer2.png" alt="texture_transfer" width="30%" />
</p>

## 5. Iterative Texture Transfer (Bells & Whistles)
I implement iterative method for texture tranfer. For eaqch iteration, alpha is calculated as: α_i = 0.8 * (i-1)/(N-1) + 0.1. Here, I uses 3 iterations for refinement.

**Parameters:**

iteration 1:
- Patch size: 25
- Alpha: 0.1

iteration 2:
- Patch size: 17
- Alpha: 0.5

iteration 3:
- Patch size: 8
- Alpha: 0.9

**Comparison Results:**
<p align="center">
  <img src="proj1_result/iter_compare1.png" alt="iter_compare" width="60%" />
</p>
<p align="center">
  <img src="proj1_result/iter_compare2.png" alt="iter_compare" width="60%" />
</p>
We can see from the result that the iterative texture transfer method has a much better result compared to the non-iterative texture transfer method.

## 6. Face-in-Toast (Bells & Whistles)

I use texture transfer to generate a version of the face with the toast texture and used a feature mask to blend between the toast texture face and the actual toast.

**Results:**
<p align="center">
  <img src="proj1_result/face_in_toast.png" alt="face_in_toast" width="100%" />
</p>

---

# Final Project 2: High Dynamic Range

In this project, there are two major components: recovering a radiance map from a collection of images and converting this radiance map into a display image.

---

### 1. Radiance Map Construction

I reconstruct an HDR radiance map from several LDR exposures based on the paper Debevec and Malik 1997.

Follow the summary below:
The observed pixel value Z_ij for pixel i in image j is a function of unknown scene radiance and known exposure duration:

$$Z_{ij} = f(E_i\Delta t_j).$$

E_i is the unknown scene radiance at pixel i, and integrating scene radiance over some time E_iΔt_j is the exposure at a given pixel. We will not solve for f, but for g = ln(f^{-1}) which maps from pixel values (from 0 to 255) to the log of exposure values:

$$g(Z_{ij}) = ln(E_i) + ln(t_j).$$

We do know that the scene radiance remains constant across the image sequence. After we have g, is it straightforward to map from the observed pixels values and shutter times to radiance by the following equation:

$$ln(E_i) = g(Z_{ij}) - ln(\Delta t_j).$$

Two additional things need to consider:
1. Second-derivative Smoothing Term
We expect g to be smooth. Debevec adds a constraint to our linear system which penalizes g according to the magnitude of its second derivative. Since g is discrete (defined only at integer values from g(0) to g(255)) we can approximate the second derivative with finite differences, e.g.:
$$g''(x) = (g(x-1) - g(x)) - (g(x) - g(x+1)) = g(x-1) + g(x+1) - 2g(x).$$
We will have one such equation for each integer in the domain of g, except for g(0) and g(255) where the second derivative would be undefined.
2. Tent Function Weighting
Each exposure only gives us trustworthy information about certain pixels. For dark pixels the relative contribution of noise is high and for bright pixels the sensor may have been saturated. To make our estimates of E_i more accurate, we need to weight the contribution of each pixel according to Equation 6 in Debevec:

$$\ln E_i = \frac{\sum_{j=1}^P w(Z_{ij})(g(Z_{ij}) - \ln \Delta t_j)}{\sum_{j=1}^P w(Z_{ij})}$$

**Results:**

Arch:
<p align="center">
  <img src="proj2_result/arch_plot.png" alt="arch" width="70%" />
  <img src="proj2_result/arch_rad.png" alt="arch" width="100%" />
</p>

Chapel:
<p align="center">
  <img src="proj2_result/chapel_plot.png" alt="chapel" width="70%" />
  <img src="proj2_result/chapel_rad.png" alt="chapel" width="70%" />
</p>

Garden:
<p align="center">
  <img src="proj2_result/garden_plot.png" alt="garden" width="70%" />
  <img src="proj2_result/garden_rad.png" alt="garden" width="100%" />
</p>

House:
<p align="center">
  <img src="proj2_result/house_plot.png" alt="house" width="70%" />
  <img src="proj2_result/house_rad.png" alt="house" width="70%" />
</p>

Bonsai:
<p align="center">
  <img src="proj2_result/bonsai_plot.png" alt="bonsai" width="70%" />
  <img src="proj2_result/bonsai_rad.png" alt="bonsai" width="100%" />
</p>

Mug:
<p align="center">
  <img src="proj2_result/mug_plot.png" alt="mug" width="70%" />
  <img src="proj2_result/mug_rad.png" alt="mug" width="100%" />
</p>

## 2. Tone Mapping Operators

We've successfully created the radiance map. Now, we wish to show detail in dark and bright image regions on a low-dynamic-range display. 
I implement a simplified version of *Durand 2002*. The steps are roughly as follows:

1. Input is linear RGB values of radiance.

2. Compute the average intensity *I* by averaging the color channels per pixel of the output radiance map.

3. Compute the chrominance channels: *R/I*, *G/I*, *B/I*

4. Compute the log intensity: $$E = \log_2(I)$$

5. Filter that with a bilateral filter to produce the 'large scale' intensity: $$B = bf(E)$$

6. Compute the detail layer: $$D = E - B$$

7. Apply an offset and a scale to the base: $$B' = (B - o) * s$$
   1. The offset is such that the maximum intensity of the base is 1. Since the values are in the log domain, $$o = max(B)$$
   2. The scale is set so that the output base has dR stops of dynamic range, i.e., $$s = dR/(max(B) - min(B))$$ 
      Try values between 2 and 8 for *dR*, that should cover an interesting range. Values around 4 or 5 should look fine.

8. Reconstruct the log intensity: $$O = 2^{(B'+D)}$$

9. Put back the colors: $$R', G', B' = O * (R/I, G/I, B/I)$$

10. Apply gamma compression. Without gamma compression the result will look too dark. Values around 0.5 should look fine (e.g., result^0.5). You can also apply the simple global intensity scaling to your final output.

**Results:**

Arch:
<p align="center">
  <img src="proj2_result/arch_result.png" alt="arch" width="100%" />
</p>

Chapel:
<p align="center">
  <img src="proj2_result/chapel_result.png" alt="chapel" width="90%" />
</p>

Garden:
<p align="center">
  <img src="proj2_result/garden_result.png" alt="garden" width="100%" />
</p>

House:
<p align="center">
  <img src="proj2_result/house_result.png" alt="house" width="90%" />
</p>

Bonsai:
<p align="center">
  <img src="proj2_result/bonsai_result.png" alt="bonsai" width="100%" />
</p>

Mug:
<p align="center">
  <img src="proj2_result/mug_result.png" alt="mug" width="100%" />
</p>
