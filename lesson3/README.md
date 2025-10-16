# Face Detection with MTCNN — README.md

## 🧠 Project Overview

This project demonstrates **face detection** using the **MTCNN (Multi-task Cascaded Convolutional Neural Network)** model in Python. The workflow involves extracting frames from a video, detecting faces, plotting bounding boxes and facial landmarks, cropping out detected faces, and preparing them for later use in facial recognition or verification tasks.

The work is part of a practical assignment from **WorldQuant University’s Applied Data Science Lab**.

---

## 📁 Project Structure

```
project4/
│
├── data/
│   ├── extracted_frames/     # Frames extracted from the input video
│   ├── images/
│   │   ├── mary_kom/         # Frames of subject Mary Kom
│   │   └── ranveer/          # Frames of interviewer Ranveer
│
├── face_detection.ipynb      # Jupyter notebook for this lesson
└── README.md                 # Project documentation
```

---

## ⚙️ Key Dependencies

* **Python 3.11+**
* **torch** — PyTorch deep learning framework
* **torchvision** — image utilities
* **facenet-pytorch** — MTCNN and InceptionResnetV1 models
* **matplotlib** — plotting and visualization
* **PIL (Pillow)** — image loading and manipulation
* **shutil** — file operations
* **pathlib** — modern file path management

---

## 🚀 Workflow Summary

### 1. Extract Frames from a Video

Frames are extracted from the video using OpenCV and saved in the `extracted_frames` directory.

```python
n_extracted_frames = len(list(frames_dir.iterdir()))
print(f"We saved {n_extracted_frames} frames.")
```

✅ This ensures the number of frames is counted correctly as an integer.

---

### 2. Load and Display a Sample Frame

A frame is loaded using Pillow to visually confirm extraction:

```python
sample_image = Image.open(extracted_frames_dir / "frame_320.jpg")
sample_image
```

---

### 3. Detect Faces Using MTCNN

MTCNN is used to detect faces, returning bounding boxes and probabilities:

```python
boxes, probs = mtcnn.detect(sample_image)
print(boxes.shape)  # e.g., (3, 4)
```

✅ Three faces detected with high confidence (≥ 0.99).

---

### 4. Plot Bounding Boxes

Bounding boxes are plotted using Matplotlib:

```python
for box in boxes:
    rect = plt.Rectangle((box[0], box[1]), box[2]-box[0], box[3]-box[1], fill=False, color='blue')
    ax.add_patch(rect)
```

---

### 5. Extract Facial Landmarks

Facial landmarks (eyes, nose, mouth corners) are extracted:

```python
boxes, probs, landmarks = mtcnn.detect(sample_image, landmarks=True)
print(landmarks.shape)  # (3, 5, 2)
```

Each detected face has 5 landmarks, each with (x, y) coordinates.

---

### 6. Plot Bounding Boxes and Landmarks Together

```python
for box, landmark in zip(boxes, landmarks):
    rect = plt.Rectangle((box[0], box[1]), box[2]-box[0], box[3]-box[1], fill=False, color='blue')
    ax.add_patch(rect)
    for point in landmark:
        ax.plot(point[0], point[1], marker='o', color='red')
```

✅ This overlays both bounding boxes and facial landmarks.

---

### 7. Crop Out Detected Faces

MTCNN can directly return cropped face tensors:

```python
faces = mtcnn(sample_image)
print(faces.shape)  # torch.Size([3, 3, 160, 160])
```

---

### 8. Visualize Cropped Faces

Using `torchvision.utils.make_grid` to create a grid of faces:

```python
Grid = make_grid(faces, nrow=3)
plt.imshow(Grid.permute(1, 2, 0).int())
plt.axis('off')
```

---

### 9. Organize Images into Directories

We prepare directories for the two subjects:

```python
images_dir = curr_work_dir / "project4" / "data" / "images"
images_dir.mkdir(exist_ok=True)

mary_kom_dir = images_dir / "mary_kom"
mary_kom_dir.mkdir(exist_ok=True)

ranveer_dir = images_dir / "ranveer"
ranveer_dir.mkdir(exist_ok=True)
```

Then, we copy selected images for each subject using `shutil.copy()`.

✅ `mary_kom/` — 5 frames of Mary Kom
✅ `ranveer/` — 5 frames of interviewer Ranveer

---

## 🧩 Key Concepts Reinforced

* **Face Detection** using MTCNN
* **Facial Landmark Localization**
* **Bounding Box Visualization**
* **Face Cropping** for recognition tasks
* **Image Preprocessing and Organization**

---

## 🏁 Final Output

* Successfully detected and visualized faces and landmarks.
* Cropped faces stored as PyTorch tensors.
* Clean and structured image dataset ready for **Face Recognition (Lesson 5)**.

---

## 📜 License

This project © 2024 by [WorldQuant University](https://www.wqu.edu/) is licensed under the [CC BY-NC-ND 4.0 License](https://creativecommons.org/licenses/by-nc-nd/4.0/).
