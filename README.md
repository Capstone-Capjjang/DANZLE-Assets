# DANZLE-Assets

## 💡 Project Overview

This repository provides **media preprocessing tools and sample assets** for the DANZLE dance training system.  
It covers two distinct but complementary pipelines that support user interaction during dance practice:

1. **Expert choreography silhouette generation** using SAM2  
2. **Avatar-based 3D dance guide** using Unity

These assets are **not part of the live backend/frontend service**, but are essential for creating user-facing content.  
Users can either:

- Follow a **transparent silhouette video** of expert dance overlaid on their camera feed, or  
- **Dance alongside a 3D avatar** rendered in real-time via Unity integration.


<pre><code>## 📁 Directory Structure ``` Danzle-assets/ ├── SAM2/ # Silhouette video generation tool │ ├── sam2_generate.py # PyTorch-based script (requires GPU) │ ├── requirements.txt │ └── sample_input/ # Sample dance images or video frames │ └── UNITY/ # Unity assets for avatar choreography rendering ├── processed_videos/ # Pre-rendered silhouette videos (.mp4) └── suisei_vivideba_motion_.fbx # Dance motion animation (FBX format) ``` </code></pre>


## ⚙️SAM2 Tech Stacks

The `SAM2/` directory contains a preprocessing pipeline built on Meta AI’s [Segment Anything Model 2 (SAM2)](https://github.com/facebookresearch/sam2).  
It extracts **binary masks** from each frame of a dance video and produces a transparent `.mp4` or `.webm` silhouette video for user guidance.

| Component          | Description                                          |
|--------------------|------------------------------------------------------|
| Model              | SAM2 (Segment Anything Model 2 by Meta AI)           |
| Framework          | PyTorch                                              |
| Input              | Individual dance frames from expert videos           |
| Output             | Binary masks and transparent silhouette `.mp4` video |
| Purpose            | Provides clean silhouette overlay for user guidance  |
| Environment        | CUDA-enabled GPU recommended                         |

📝 *For advanced use (e.g., Colab, neon visualization), refer to [`SAM2/README.md`](./SAM2/README.md).*

---

## ⚙️Unity Tech Stacks

The `UNITY/` directory includes Unity project files, silhouette references, and motion assets used to render a **3D avatar** performing expert choreography.  
This module enables the **"dance-with-avatar" mode** by generating pre-rendered avatar videos that are later displayed on the user's camera view during practice.  
It may also include `.fbx` motion files that define expert choreography, which can be applied to humanoid avatars in Unity.

| Component | Description                                                             |
|-----------|-------------------------------------------------------------------------|
| Engine    | Unity 2022.3 LTS                                                        |
| Input     | Silhouette videos or motion data (.fbx)                                 |
| Output    | Avatar character performing choreography in 3D                          |
| Purpose   | Creates an immersive experience by letting users dance with a 3D avatar |
| Platform  | Output is integrated into user-facing camera UI in the app              |

📝 *Used to generate interactive content for “challenge” mode.*


## 📍Features

- Converts expert choreography videos into **transparent silhouette guides** using SAM2
- Renders **3D avatar-based dance guidance** using Unity
- Output visuals are optimized for overlay in mobile camera view
- Includes FFmpeg-based tools to convert videos into `.mp4` or `.webm` with alpha transparency
- Sample input frames and output videos are included for testing and prototyping


## 🚀 How to Run (SAM2 Module)

```bash
# 1. Clone and navigate
git clone https://github.com/Capstone-Capjjang/DANZLE-Assets.git
cd DANZLE-Assets/SAM2

# 2. (Optional) Set up virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run silhouette generation
python sam2_generate.py --input sample_input/frame_*.png --output out.mp4

---

## 🔐 Environment Variables

- No `.env` file is required.
- Input/output file paths are passed via CLI or hardcoded in `sam2_generate.py`.
- For best performance, install **PyTorch with CUDA** support.

---

## 📝 Additional Notes

- `conversion_tool/` includes FFmpeg scripts for `.webm` alpha encoding if needed.
- Colab-based interactive pipeline (with point-click masking and neon effects) is available in `SAM2/README.md`.
- Ensure silhouette and avatar videos are rendered at **consistent resolution and framerate**.

---

## 📦 Sample Assets

| Type           | Location                    |
|----------------|-----------------------------|
| Input Frames   | `SAM2/sample_input/`        |
| Output Video   | `UNITY/processed_videos/`   |
| Scripts        | `SAM2/sam2_generate.py`     |











