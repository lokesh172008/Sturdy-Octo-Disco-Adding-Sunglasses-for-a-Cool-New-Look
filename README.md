# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.


## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!
### Code
```
Name: K.Lokesh Achari
Reg: 212225040208

```
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('christian-bale.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")


faceImage.shape
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1])
plt.title("sunglassesPNG")

glassBGR = sunglassesPNG[:,:,0:3]
glassMask1 = sunglassesPNG[:,:,3]

plt.figure(figsize=[15,15])

plt.figure(figsize=[15,15])

# Show sunglasses color channels
plt.subplot(121)
plt.imshow(glassBGR[:,:,::-1])  # BGR → RGB
plt.title('Sunglass Color channels')

# Create grayscale and threshold to make mask
glassGray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask1 = cv2.threshold(glassGray, 240, 255, cv2.THRESH_BINARY_INV)  # detect non-white

# Show generated mask
plt.subplot(122)
plt.imshow(glassMask1, cmap='gray')
plt.title('Sunglass Mask (generated)')


import cv2
import mediapipe as mp
import numpy as np
import matplotlib.pyplot as plt

# Load images
faceImage = cv2.imread("christian-bale.jpg")
glassPNG = cv2.imread("sunglass.png", cv2.IMREAD_UNCHANGED)


# --- Step 1: Detect face landmarks ---
mp_face = mp.solutions.face_mesh
face_mesh = mp_face.FaceMesh(static_image_mode=True, max_num_faces=1)

rgb_img = cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB)
results = face_mesh.process(rgb_img)

h, w, _ = faceImage.shape

if results.multi_face_landmarks:
   for face_landmarks in results.multi_face_landmarks:
       # Get left & right eye corner points (approx landmarks)
       left_eye = face_landmarks.landmark[33]   # left eye outer
       right_eye = face_landmarks.landmark[263] # right eye outer

       # Convert to pixel coordinates
       x1, y1 = int(left_eye.x * w), int(left_eye.y * h)
       x2, y2 = int(right_eye.x * w), int(right_eye.y * h)

       # Compute sunglasses width based on eye distance
       eye_width = x2 - x1
       new_w = int(eye_width * 2.0)   # make glasses wider than eyes
       new_h = int(new_w * glassPNG.shape[0] / glassPNG.shape[1])

       # Resize sunglasses
       glass_resized = cv2.resize(glassPNG, (new_w, new_h))

       # Create mask
       glass_gray = cv2.cvtColor(glass_resized, cv2.COLOR_BGR2GRAY)
       _, mask = cv2.threshold(glass_gray, 240, 255, cv2.THRESH_BINARY_INV)
       mask_inv = cv2.bitwise_not(mask)

       # Position (centered around eyes)
       x = x1 - int(new_w * 0.25)
       y = y1 - int(new_h * 0.4)

       # ROI on face
       roi = faceImage[y:y+new_h, x:x+new_w]

       # Blend sunglasses with ROI
       bg = cv2.bitwise_and(roi, roi, mask=mask_inv)
       fg = cv2.bitwise_and(glass_resized, glass_resized, mask=mask)
       combined = cv2.add(bg, fg)

       faceImage[y:y+new_h, x:x+new_w] = combined

# Show result
plt.figure(figsize=[10,10])
plt.imshow(cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB))
plt.title("Face with Sunglasses (Auto Aligned)")
plt.axis("off")
plt.show()
```
### Output
<img width="410" height="432" alt="638196920-62b09deb-244f-4d90-914c-5e9119be5741" src="https://github.com/user-attachments/assets/3fb7b846-56af-4a4a-97f2-e3885b057d51" />
<img width="567" height="566" alt="638200196-6900540c-695d-4d52-8f59-b147f5c3d48f" src="https://github.com/user-attachments/assets/2bb3dea0-d1eb-4518-9ba1-d17025c92c20" />
<img width="1442" height="676" alt="638197857-04155b25-6830-4a7d-b89d-27f6f31366a5" src="https://github.com/user-attachments/assets/0b400771-3cd6-45c8-ac3b-1c7622e79024" />
<img width="627" height="627" alt="638200764-e6a24e7e-5114-4601-9c10-f66b77b19d21" src="https://github.com/user-attachments/assets/04f791b5-4d4c-46eb-8f0b-b5b0b2adbc2d" />

### Result
Program for adding Sunglasses to a Passport Photo Using OpenCV, Successfully executed

