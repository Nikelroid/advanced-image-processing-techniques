
# VisionLab: Advanced-Image-Processing-Techniques

![Python](https://img.shields.io/badge/python-3.8%2B-blue?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-1.24%2B-013243?logo=numpy&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.5%2B-red?logo=opencv&logoColor=white)


## Description
This repository contains a collection of fundamental computer vision and image processing algorithms implemented from scratch in Python. The project moves beyond basic library calls, focusing on the mathematical implementation of techniques such as Frequency Domain filtering, manual Homography matrix calculation, and Hybrid Image synthesis.

The goal is to demonstrate a deep understanding of how digital images can be manipulated in both spatial and frequency domains to achieve results like sharpening, object detection, perspective rectification, and optical illusions.

## Features
* **Image Sharpening (Spatial & Frequency Domains):** Implements four distinct sharpening methods:
    * Unsharp Masking using Gaussian Blur.
    * Laplacian of Gaussian (LoG) filtering.
    * High-pass filtering in the Fourier Domain.
    * Laplacian filtering in the Fourier Domain (UV transformation).
* **Robust Template Matching:** A manual implementation of Normalized Cross-Correlation (NCC) that can handle noise and potential scaling differences to detect objects (columns) within a scene.
* **Perspective Correction (Homography):** A tool to rectify perspective distortion. It manually calculates the Homography matrix by solving the linear system $Ah=b$ and performs inverse mapping with bilinear interpolation.
* **Hybrid Images:** Generates optical illusions by combining the low-frequency components of one image with the high-frequency components of another, creating an image that changes interpretation based on viewing distance.

## File Descriptions & Implementation Details

### 1. `q1.py` - Image Sharpening
This script applies various sharpening filters to a blurred input image (`flowers.blur.png`).
* **Methods:**
    * `gaussian_sharpening`: Calculates $f + \alpha(f - f * G)$ using a generated Gaussian kernel.
    * `laplacian_sharpening`: Convolves the image with a generated Laplacian kernel.
    * `fourier_highpass_sharpening`: Multiplies the image spectrum with a high-pass filter mask.
    * `fourier_uv_sharpening`: Sharpens using the property that the Laplacian in the frequency domain corresponds to multiplication by $4\pi^2(u^2+v^2)$.
* **Output:** Generates intermediate and final results (`res01.jpg` - `res14.jpg`).

### 2. `q2.py` - Template Matching
Detects specific architectural features (columns) in a seascape image.
* **Logic:** Preprocesses the template using Canny edge detection to refine the region of interest. It then slides the template over the image, calculating a correlation score to find matches.
* **Key Feature:** Implements a custom correlation loop rather than relying solely on `cv2.matchTemplate`.
* **Output:** Draws bounding boxes around detected columns (`res29.jpg` / `res15.jpg`).


### 3. `q3.py` - Homography & Image Warping
An interactive script to correct the perspective of a book cover.
* **Interaction:** Double-click 4 corners of an object in the image to define the source points.
* **Algorithm:**
    1.  Calculates the destination width/height based on the aspect ratio of selected points.
    2.  Constructs the matrix $A$ and solves $Ah=b$ to find the Homography matrix $H$.
    3.  Performs **Inverse Mapping**: Iterates over destination pixels, multiplies by $H^{-1}$ to find source coordinates, and applies **Bilinear Interpolation** for pixel values.
* **Output:** Displays the rectified, flat view of the book (`res18.jpg`).


### 4. `q4.py` - Hybrid Images
Combines a near-field image (e.g., a Parrot) and a far-field image (e.g., an Eagle).
* **Alignment:** Uses affine transformations to align features (like eyes/beak) of the two images.
* **Synthesis:**
    1.  Converts images to the Frequency Domain (DFT).
    2.  Applies a Gaussian Low-pass filter to one image.
    3.  Applies a Gaussian High-pass filter ($1 - Lowpass$) to the other.
    4.  Combines them and computes the Inverse DFT.
* **Output:** An image that looks like one object up close and another from afar (`res30-hybrid-near.jpg`, `res31-hybrid-far.jpg`).


## Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/nikelroid/image-processing-2.git](https://github.com/nikelroid/image-processing-2.git)
    cd image-processing-2
    ```

2.  **Install dependencies:**
    ```bash
    pip install numpy opencv-python
    ```

## Usage

Ensure the input images (`flowers.blur.png`, `Greek-ship.jpg`, `books.jpg`, `raw1.jpg`, `raw2.jpg`) are in the same directory as the scripts.

**Sharpening:**
```bash
python q1.py
````

**Template Matching:**

```bash
python q2.py
```

**Homography (Interactive):**

```bash
python q3.py
```

  * *Instructions:* Double-click the four corners of a book in the window that appears. Order: Top-Left -\> Top-Right -\> Bottom-Right -\> Bottom-Left (counter-clockwise or as required by the logic). Press `Esc` to exit.

**Hybrid Images:**

```bash
python q4.py
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is open-source and available under the **MIT License**.

## Contact

If you have questions about the mathematical implementations or the report, please open an issue in the repository.

