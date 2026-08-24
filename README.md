**Experiment 7 – Record – Hough Transform**

# Hough Transform – Line Detection

## Aim

To implement a basic line detection system using the **Hough Transform** technique in OpenCV by detecting edges in an image and identifying straight lines present in the image.

---

## Experiment Details

* **Experiment No.:** 7
* **Experiment Name:** Record – Hough Transform
* **Name:** Sabarish A
* **Register No.:** 212225230232

---

## Learning Objective

The objective of this experiment is to:

* Understand the concept of line detection in digital images.
* Learn how to use OpenCV for image processing.
* Convert a color image into grayscale.
* Detect edges using the Canny edge detector.
* Detect straight lines using the Probabilistic Hough Transform.
* Draw the detected lines on the original image.
* Understand the basic stages of a computer vision pipeline.

---

## Software Used

* Python
* Jupyter Notebook / VS Code
* OpenCV (`cv2`)
* NumPy
* Matplotlib

---

## Libraries Used

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### OpenCV

OpenCV is used for image processing operations such as:

* Reading the image
* Converting the image to grayscale
* Performing Canny edge detection
* Detecting lines using the Hough Transform
* Drawing detected lines

### NumPy

NumPy is used for numerical operations and for handling the coordinates returned by the Hough Transform.

### Matplotlib

Matplotlib is used to display the input image, grayscale image, Canny edge output, and final Hough Transform result.

---

# Algorithm

### Step 1: Import Required Libraries

Import OpenCV, NumPy, and Matplotlib.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

### Step 2: Load the Image

The input image is loaded using the `cv2.imread()` function.

```python
image = cv2.imread('bus.jpg')
```

The notebook uses **`bus.jpg`** as the input image.

---

### Step 3: Convert Image to Grayscale

The color image is converted from BGR format to grayscale using:

```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

Grayscale conversion simplifies the image and provides a single intensity value for each pixel.

---

### Step 4: Display the Input and Grayscale Images

The original image is converted from OpenCV's BGR format to RGB before displaying it using Matplotlib.

```python
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Input Image")
plt.axis('off')
```

The grayscale image is displayed using:

```python
plt.imshow(gray_image, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')
```

---

### Step 5: Perform Canny Edge Detection

The Canny operator is used to detect edges in the grayscale image.

```python
edges = cv2.Canny(gray_image, 50, 150)
```

The two threshold values used are:

* Lower threshold = **50**
* Upper threshold = **150**

The resulting edge image contains the important boundaries and edges detected in the image.

---

### Step 6: Detect Lines Using Hough Transform

The **Probabilistic Hough Transform** is applied using `cv2.HoughLinesP()`.

```python
lines = cv2.HoughLinesP(
    edges,
    1,
    np.pi / 180,
    100,
    minLineLength=50,
    maxLineGap=10
)
```

The parameters used are:

| Parameter        |         Value | Description                                 |
| ---------------- | ------------: | ------------------------------------------- |
| Image            |       `edges` | Canny edge image                            |
| Resolution       |           `1` | Distance resolution                         |
| Angle resolution | `np.pi / 180` | 1-degree angular resolution                 |
| Threshold        |         `100` | Minimum number of votes                     |
| `minLineLength`  |          `50` | Minimum accepted line length                |
| `maxLineGap`     |          `10` | Maximum gap between connected line segments |

---

### Step 7: Draw Detected Lines

The coordinates returned by `HoughLinesP()` are used to draw lines on the original image.

```python
if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = np.array(line).flatten()

        cv2.line(
            image,
            (int(x1), int(y1)),
            (int(x2), int(y2)),
            (0, 255, 0),
            2
        )
```

Each detected line is drawn using a line thickness of **2 pixels**.

---

### Step 8: Display the Final Result

The final image containing the detected lines is displayed using Matplotlib.

```python
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Result of Hough Transform")
plt.axis('off')
```

---

# Complete Code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Load the image using imread() from cv2 module
image = cv2.imread('bus.jpg')

# Step 3: Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Display Input Image
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Input Image")
plt.axis('off')

# Display Grayscale Image
plt.imshow(gray_image, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')

# Step 4: Using Canny operator from cv2, detect the edges
edges = cv2.Canny(gray_image, 50, 150)

# Display Canny Edge Detector output
plt.imshow(edges, cmap='gray')
plt.title("Canny Edge Detector")
plt.axis('off')

# Step 5: Detect line coordinates using HoughLinesP()
lines = cv2.HoughLinesP(
    edges,
    1,
    np.pi / 180,
    100,
    minLineLength=50,
    maxLineGap=10
)

# Step 6: Draw detected lines on the original image
if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = np.array(line).flatten()

        cv2.line(
            image,
            (int(x1), int(y1)),
            (int(x2), int(y2)),
            (0, 255, 0),
            2
        )

# Display the result
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Result of Hough Transform")
plt.axis('off')
```

---

# Working Principle

The complete process can be represented as:

```text
Input Image
     ↓
Grayscale Conversion
     ↓
Canny Edge Detection
     ↓
Edge Image
     ↓
Probabilistic Hough Transform
     ↓
Detected Line Coordinates
     ↓
Draw Lines on Original Image
     ↓
Final Output
```

The notebook follows this sequence directly: image loading → grayscale conversion → Canny edge detection → `HoughLinesP()` → drawing the detected lines → displaying the result. 

---

# Expected Output

The program produces the following outputs:

### 1. Input Image

Displays the original `bus.jpg` image.
<img width="520" height="550" alt="image" src="https://github.com/user-attachments/assets/9d3b72af-340e-450f-9a44-7334de1b4a23" />



### 2. Grayscale Image

Displays the input image converted into grayscale.
<img width="698" height="546" alt="image" src="https://github.com/user-attachments/assets/c14b0276-7f3d-4484-8444-7c6c5bfeb4db" />


### 3. Canny Edge Detector

Displays the edges detected using the Canny operator.
<img width="508" height="549" alt="image" src="https://github.com/user-attachments/assets/f782586c-8a3e-45a0-8a21-7d2f09f1eb9e" />


### 4. Result of Hough Transform

<img width="523" height="523" alt="image" src="https://github.com/user-attachments/assets/be6537d1-4d54-4e4a-a9a0-18b801eb72cf" />

Displays the original image with detected straight lines drawn over it.


---

# Applications

Hough Transform-based line detection can be used in various computer vision applications, including:

* Lane detection
* Road boundary detection
* Document and shape analysis
* Industrial inspection
* Object detection
* Structural feature detection
* Image segmentation
* Computer vision-based navigation

---

# Advantages

* Simple and effective method for detecting straight lines.
* Available directly in OpenCV.
* Works well with edge-detected images.
* Probabilistic Hough Transform can efficiently detect line segments.
* Useful as a preprocessing stage for more advanced computer vision applications.

---

# Limitations

* The result depends on the selected threshold values.
* Incorrect Canny thresholds can produce unwanted edges.
* Hough Transform parameters need to be selected appropriately.
* Complex or noisy images may produce unwanted line detections.
* The implementation in this experiment detects general straight lines rather than specifically identifying road lanes.

---

# Result

Thus, the **Hough Transform-based line detection system** was successfully implemented using OpenCV. The input image was converted into grayscale, edges were detected using the Canny edge detector, and straight line segments were identified using the **Probabilistic Hough Transform (`HoughLinesP`)**. The detected lines were successfully drawn on the original image and displayed as the final output.

---

## Developed By

**Name:** Sabarish A
**Register No:** 212225230232
