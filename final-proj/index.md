# Final Project 1:Image Quilting
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
