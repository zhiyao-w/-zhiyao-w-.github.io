# Project: Image Warping and Mosaicing
Zhiyao Wang

The project explores various aspects of image warping, including homography computation, image rectification, and the creation of  image mosaics through projective transformations and blending techniques.

---

## Part 1: Shoot the Pictures
Here is the picture I shoot and used in this project:
</p>
<p align="center">
  <img src="1b.jpg" alt="Smiling" width="20%" />
  <img src="11b.jpg" alt="Smiling" width="20%" />
  <img src="43b.jpg" alt="Smiling" width="20%" />
</p>


---

## Part 2: Recovering Homographies

### Objective
To align multiple images into a single mosaic, it is crucial to determine the homographic transformations between them. A homography maps points from one image to another, enabling the warping and alignment necessary for seamless mosaicing.

### Theory
A homography relates the coordinates of corresponding points between two images through a 3x3 matrix **H**:

\[
\mathbf{q} = \mathbf{H} \mathbf{p}
\]

where:
- \(\mathbf{q}\) and \(\mathbf{p}\) are points in homogeneous coordinates.
- **H** is the homography matrix with 8 degrees of freedom (the last element is typically set to 1 for normalization).

Expanding the equation, we obtain a system of linear equations that can be solved to determine the elements of **H**. With more than four point correspondences, the system becomes overdetermined, and least-squares methods can be employed to find an optimal solution.

### Method
- **Point Correspondences**: Identified corresponding points between image pairs using a mouse-clicking interface. Ensured high accuracy in point selection to maintain stability in homography recovery.
- **Linear System Setup**: Formulated a linear system based on the homography equations derived from the point correspondences. Each pair of points contributes two equations to the system.
- **Least-Squares Solution**: Solved the overdetermined system using least-squares optimization to obtain the homography matrix **H**. Normalized the matrix by setting the last element to 1 to maintain scale consistency.

### Results
Successfully recovered homography matrices that accurately align key points between image pairs. This alignment facilitates precise image warping in the next stages of the project.

---

## Part 3: Warping the Images

### Objective
To align images based on the computed homographies, enabling their integration into a cohesive mosaic. This involves transforming each image's perspective to match a reference frame.

### Method
- **Inverse Warping**: Mapped coordinates from the output image back to the input image using the inverse of the homography matrix. This approach ensures that each pixel in the output image corresponds to a valid location in the input image.
- **Interpolation**: Applied linear interpolation to resample pixel values, ensuring smooth transitions and avoiding aliasing artifacts. Utilized efficient interpolation techniques to handle multiple color channels.
- **Bounding Box Calculation**: Determined the size of the warped image by transforming the original image's corners and computing the resulting bounding box. This step ensures that the entire warped image fits within the output canvas.
- **Vectorization**: Implemented the warping process without explicit loops, leveraging vectorized operations for computational efficiency.

### Results
Produced rectified images by transforming the perspectives of the original images. The rectified images demonstrate accurate alignment and preservation of structural details, validating the effectiveness of the homography and warping processes.

![Original Image](original_image.png)
*Original Image*

![Rectified Image](rectified_image.png)
*Rectified Image*

---

## Part 4: Blending Images into a Mosaic

### Objective
To seamlessly combine multiple warped images into a single mosaic, ensuring smooth transitions and minimizing visible seams.

### Method
- **Alignment**: Utilized the computed homographies to align all images to a common reference frame. This alignment ensures that overlapping regions correspond accurately between images.
- **Blending**: Applied alpha blending techniques to merge overlapping regions. By adjusting the transparency of overlapping pixels, the blending process reduces visible seams and creates a cohesive appearance.
- **Compositing**: Stacked the aligned images onto a unified canvas, carefully handling spatial relationships and overlaps. Managed image boundaries to maintain integrity and avoid ghosting effects.

### Results
Created three distinct mosaics by blending different sets of images. Each mosaic showcases seamless integration of the source images, with smooth transitions and minimal artifacts, demonstrating the effectiveness of the homography computation and blending techniques.

![Mosaic 1](mosaic1.png)
*Mosaic Example 1*

![Mosaic 2](mosaic2.png)
*Mosaic Example 2*

![Mosaic 3](mosaic3.png)
*Mosaic Example 3*

---

## Optional: Bells and Whistles

### Objective
Enhance the basic mosaicing functionality with additional features that improve the quality and aesthetics of the final mosaic.

### Enhancements
- **Seam Optimization**: Implemented seam finding algorithms to identify optimal paths for blending, minimizing visible transitions between images.
- **Multi-band Blending**: Applied multi-band blending techniques to handle different frequency components of the images, resulting in more natural and artifact-free merges.
- **Interactive Interface**: Developed an interactive user interface for selecting point correspondences, streamlining the homography computation process and improving user experience.

### Results
Enhanced the mosaicing process with optimized seams and multi-band blending, resulting in higher-quality mosaics with fewer visible artifacts. The interactive interface facilitated easier point selection, making the homography computation more efficient and user-friendly.

![Enhanced Mosaic](enhanced_mosaic.png)
*Enhanced Mosaic Example*

---

## Submission

All project components, including the code, images, and documentation, have been compiled and are ready for submission. The repository includes:

- **Source Code**: Python scripts for homography computation, image warping, and blending.
- **Captured Images**: Original and processed images used for creating the mosaics.
- **Results**: Final mosaics and intermediate outputs demonstrating each project's stage.
- **Documentation**: This portfolio detailing the methods, implementations, and results.

---

## References

- **Project Instructions**: [Assignment Description](#)
- **Homography Theory**: [Multiple View Geometry by Hartley and Zisserman](https://www.amazon.com/Multiple-View-Geometry-Computer-Vision/dp/0521540518)
- **Image Processing Libraries**:
  - [OpenCV](https://opencv.org/)
  - [NumPy](https://numpy.org/)
  - [SciPy](https://scipy.org/)
  - [Matplotlib](https://matplotlib.org/)

