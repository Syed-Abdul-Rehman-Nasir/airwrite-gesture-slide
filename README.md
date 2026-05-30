# AirWrite & Gesture Slide

> **Touchless hand gesture control** for real-time air drawing and presentation navigation — OpenCV · MediaPipe · Python

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.5%2B-5C3EE8?logo=opencv&logoColor=white)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Hands-00897B)](https://mediapipe.dev/)
[![License](https://img.shields.io/badge/License-MIT-green)]()

---

## What Is AirWrite & Gesture Slide?

A real-time computer vision system that turns your webcam and bare hand into a touchless input device. Point your index finger to draw in mid-air on a live camera feed, or wave to navigate presentation slides — no mouse, stylus, or touchscreen required.

Built with **MediaPipe Hands** for 21-point landmark detection and **OpenCV** for rendering, it runs entirely on a standard webcam at real-time frame rates.

---

## Modules

### ✍️ Virtual Painter
Draw directly onto the live camera feed using hand gestures.

| Gesture | Action |
|---------|--------|
| ☝️ Index finger only | Draw on canvas |
| ☝️✌️ Index + middle fingers | Selection / hover mode |
| ✊ Fist | Clear / stop drawing |

How it works: landmarks from MediaPipe track the fingertip position each frame; a persistent canvas layer is alpha-blended over the camera feed so strokes accumulate naturally.

### 🖥️ Gesture Slide
Control a presentation without touching a keyboard or remote.

| Gesture | Action |
|---------|--------|
| 👍 Thumb only (hand raised) | Previous slide |
| 🤙 Pinky only (hand raised) | Next slide |
| ☝️ Index finger | Draw annotation on current slide |
| ☝️✌️ Index + middle | Pointer / laser mode |
| ✌️🤙 Three fingers | Undo last annotation |

Slides are loaded from a local folder of images. A gesture threshold line divides the camera frame — navigation gestures are only triggered when the hand is raised above it, preventing accidental swipes mid-annotation.

---

## How It Works

```
Webcam frame (BGR)
      │
      ▼
  BGR → RGB conversion (OpenCV)
      │
      ▼
  MediaPipe Hands
  21 landmarks per hand · up to 2 hands
      │
      ├── fingersUp()   →  which fingers are extended
      ├── findDistance() →  distance between any two landmarks
      └── bbox + center  →  hand position in frame
      │
      ▼
  Gesture classifier
  (landmark geometry rules — no ML model needed)
      │
      ├── Virtual Painter  →  canvas overlay (cv2.line / cv2.circle)
      └── Gesture Slide    →  slide index update + annotation layer
      │
      ▼
  Rendered output frame (cv2.imshow)
```

---

## Repository Structure

```
.
├── main.py                # Entry point — runs Gesture Slide module
├── HandTrackingModule.py  # HandDetector class (MediaPipe wrapper, CVZone-style)
├── handTracker.py         # Lightweight alternate tracker (Virtual Painter)
├── requirements.txt
└── presentation/          # Place your slide images here (.jpg / .png)
```

---

## Getting Started

### Prerequisites

- Python 3.8+
- Webcam
- A folder of slide images named so they sort in order (e.g. `slide1.jpg`, `slide2.jpg`)

### Installation

```bash
git clone https://github.com/Syed-Abdul-Rehman-Nasir/airwrite-gesture-slide.git
cd airwrite-gesture-slide
pip install -r requirements.txt
```

### Run

```bash
python main.py
```

Place your presentation images inside a `presentation/` folder in the project root before running. Press `q` to quit.

---

## Tech Stack

| Library | Role |
|---------|------|
| [MediaPipe](https://mediapipe.dev/) | Real-time hand landmark detection (21 keypoints) |
| [OpenCV](https://opencv.org/) | Frame capture, drawing, display |
| NumPy | Coordinate interpolation and array ops |

No model training required — gesture recognition is built from landmark geometry rules (`fingersUp`, `findDistance`), making it fast and fully interpretable.

---

## Key Implementation Details

- **Hand type detection** — MediaPipe's handedness label is flipped to correct for mirrored webcam feeds
- **Person-aware gesture zones** — the gesture threshold line (`gestureThreshold = 300`) separates navigation gestures (hand above line) from annotation gestures (hand below), preventing accidental slide changes mid-draw
- **Coordinate remapping** — index finger x/y are remapped from camera space to slide space via `np.interp`, so annotations align correctly regardless of where in the frame the hand appears
- **Debounced button press** — a frame counter (`delay = 30`) prevents a single gesture from firing multiple slide changes

---

## Use Cases

- **Classrooms** — annotate slides and navigate hands-free during a lesson
- **Remote presentations** — gesture control without a clicker or second device
- **Assistive technology** — touch-free drawing and control interface
- **CV portfolio** — demonstrates real-time landmark tracking, gesture classification, and canvas compositing

---

## Requirements

```
opencv-python==4.5.3.56
mediapipe==0.8.7.3
numpy==1.19.2
```

Full pinned list in [`requirements.txt`](requirements.txt).
