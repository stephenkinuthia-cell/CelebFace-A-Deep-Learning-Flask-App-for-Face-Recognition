# AI Lab: Deep Learning for Computer Vision

### WorldQuant University

This project is part of the **AI Lab: Deep Learning for Computer Vision** module by [WorldQuant University](https://www.wqu.edu/). It focuses on video frame extraction and analysis using Python and computer vision tools such as OpenCV, PyTorch, and torchvision.

---

## 🧠 Objective

To learn how to:

1. Download and process video data.
2. Extract frames using OpenCV.
3. Explore video metadata (frame rate, count, and dimensions).
4. Display and transform extracted frames for deep learning applications.

---

## 📦 Dependencies

This lab uses the following libraries:

```python
import subprocess
from pathlib import Path
import cv2
import matplotlib.pyplot as plt
import pytubefix
import torch
import torchvision
from IPython.display import Video
from pytubefix import YouTube
from torchvision import transforms
from torchvision.io import read_image
from torchvision.transforms.functional import to_pil_image
from torchvision.utils import make_grid
```

Ensure all dependencies are installed in your environment:

```bash
pip install torch torchvision opencv-python matplotlib pytubefix
```

---

## ⚙️ Project Steps

### 1. Video Download and Setup

The lab begins by downloading a sample YouTube video of Indian Olympic boxer **Mary Kom** and saving it to the local directory:

```python
project_dir = Path("project4")
data_dir = "data"
video_dir = project_dir / data_dir
video_name = "mary_kom.mp4"
video_url = "https://www.youtube.com/watch?v=XScnCdyVbIU"
```

> The video is pre-included in the project files, so manual download can be skipped.

---

### 2. Trimming Video Duration

The function `cut_video()` shortens the original video using FFmpeg:

```python
def cut_video(input_file, output_file, start_time, duration):
    """Cuts a portion of a video using FFmpeg."""
    command = [
        "ffmpeg", "-ss", str(start_time), "-i", input_file,
        "-t", str(duration), "-c", "copy", output_file
    ]
    subprocess.run(command)
```

Usage:

```python
cut_video(input_video, output_video, start_time="00:00:00", duration="00:01:00")
```

---

### 3. Reading Video Metadata

```python
video_capture = cv2.VideoCapture(str(output_video))
frame_rate = video_capture.get(cv2.CAP_PROP_FPS)
frame_count = int(video_capture.get(cv2.CAP_PROP_FRAME_COUNT))
print(f"Frame rate: {frame_rate}, Total frames: {frame_count}")
```

---

### 4. Extracting Frames

Create a folder for storing extracted frames:

```python
frames_dir = video_dir / "extracted_frames"
frames_dir.mkdir(exist_ok=True)
```

Extract every 5th frame:

```python
interval = frame_rate * 0.20
frame_count = 0

while True:
    ret, frame = video_capture.read()
    if not ret:
        break
    if frame_count % int(interval) == 0:
        frame_path = frames_dir / f"frame_{frame_count}.jpg"
        cv2.imwrite(str(frame_path), frame)
    frame_count += 1
video_capture.release()
```

---

### 5. Counting Extracted Frames

```python
n_extracted_frames = len(list(frames_dir.iterdir()))
print(f"We saved {n_extracted_frames} frames.")
```

---

### 6. Displaying Sample Frames

```python
def display_sample_images(dir_path, sample=5):
    image_list = []
    images = sorted(dir_path.iterdir())[:sample]
    for img_path in images:
        image = read_image(str(img_path))
        resize_transform = transforms.Resize((240, 240))
        image = resize_transform(image)
        image_list.append(image)
    grid = make_grid(image_list, nrow=5)
    return to_pil_image(grid)

# Display 20 sample frames
display_sample_images(frames_dir, sample=20)
```

---

## 🧩 Key Learning Outcomes

* Mastered basic **video manipulation** with OpenCV and FFmpeg.
* Learned how to **extract and preprocess frames** for model training.
* Practiced **image visualization and transformation** with torchvision.

---

## 📜 License

This project is licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](https://creativecommons.org/licenses/by-nc-nd/4.0/).

© 2024 [WorldQuant University](https://www.wqu.edu/).
