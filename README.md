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

faceImage = cv2.imread('/content/How To Robert Downey Jr Hairstyle at Ryandreher.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="375" height="575" alt="486482576-55762833-cdf9-4ea5-a160-f155ca2529d0" src="https://github.com/user-attachments/assets/d1fb7514-2b16-4868-8dd9-bb1782991756" />
```
faceImage.shape
```

<img width="697" height="509" alt="486482654-ad2c7a02-f1e1-47a3-8f28-097c635d059f" src="https://github.com/user-attachments/assets/75d48c22-0792-4791-96fc-213a3cc7ab4d" />
```
glassPNG.shape

```
<img width="149" height="38" alt="486482667-0cc51503-a907-46b2-bfa1-7efb1f8a1dfa" src="https://github.com/user-attachments/assets/9e8d9643-db27-4a41-8f3b-57c61dccac5e" />
```
glassPNG = cv2.resize(glassPNG,(240,150))
print("image Dimension ={}".format(glassPNG.shape))
```
<img width="330" height="45" alt="486482682-53a89e42-fe44-4623-89f6-06c129531dff" src="https://github.com/user-attachments/assets/926f7706-6cff-4d75-ab37-fa69dad88331" />
```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

plt.figure(figsize=[16,16])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1627" height="526" alt="486482697-618da2bd-dade-4dcd-be48-977f49ca902a" src="https://github.com/user-attachments/assets/a5f033db-3b05-483b-9519-b552b0b507a8" />
```
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[205:355,105:345]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="448" height="556" alt="486482710-a67ccac4-e036-473b-ba4b-8119d55ad8b3" src="https://github.com/user-attachments/assets/162ec8b1-6c3b-4a54-9f6a-33d885ada490" />
```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[205:355,105:345]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
<img width="1771" height="407" alt="486482729-47d38360-d73a-4355-b692-19bccb486787" src="https://github.com/user-attachments/assets/0764b67b-07ef-4c40-ae21-82ce5db42fa5" />
```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[205:355,100:340]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="1341" height="823" alt="486482760-eace2895-92d7-49b0-b904-03d47fb14719" src="https://github.com/user-attachments/assets/4cf9014a-a274-47f0-9338-05d907306f7f" />

### Result
Program for adding Sunglasses to a Passport Photo Using OpenCV, Successfully executed

