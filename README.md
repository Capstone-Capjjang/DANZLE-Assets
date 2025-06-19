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


## 📁 Directory Structure

<pre>
Danzle-assets/<br>
├── SAM2/                         # Silhouette generation tool (Colab-based)<br>
│   ├── extractSillouet.ipynb     # Main Colab notebook for SAM2 processing<br>
│   └── SuperShy.mp4              # Sample expert choreography video<br>
│<br>
└── UNITY/                        # Unity assets for avatar choreography rendering<br>
    ├── processed_videos/         # Pre-rendered silhouette videos (.mp4)<br>
    │   └── challenge_avatar.mp4  # Sample Unity output video (optional)<br>
    └── suisei_vivideba_motion_.fbx  # Dance motion animation (FBX format)<br>
</pre>


## ⚙️ SAM2 Tech Stacks

The `SAM2/` directory contains a preprocessing pipeline built on Meta AI’s [Segment Anything Model 2 (SAM2)](https://github.com/facebookresearch/sam2).  
It uses a Google Colab-based notebook to generate **silhouette masks** and apply **neon visual effects**, exporting transparent videos for user guidance.

| Component          | Description                                          |
|--------------------|------------------------------------------------------|
| Model              | SAM2 (Segment Anything Model 2 by Meta AI)           |
| Framework          | PyTorch (via Colab)                                  |
| Input              | Expert choreography video frames or video            |
| Output             | Silhouette masks and transparent `.webm` video       |
| Purpose            | Provides visual guidance through minimal silhouettes |
| Platform           | Google Colab + Drive                                 |

📝 *See [`SAM2/README.md`](./SAM2/README.md) for step-by-step Colab instructions.*

---

## ⚙️ Unity Tech Stacks

The `UNITY/` directory includes motion data and pre-rendered output for visualizing a **3D avatar** that performs expert choreography in Unity.  
This module powers the **"dance-with-avatar" mode**, where an animated avatar is shown alongside the user’s camera feed during dance practice.  
The `.fbx` motion file defines choreography, while the `.mp4` sample video demonstrates the intended visual result in Unity.

| Component | Description                                                             |
|-----------|-------------------------------------------------------------------------|
| Engine    | Unity 2022.3 LTS                                                        |
| Input     | Motion data (.fbx), sample output videos (.mp4)                         |
| Output    | Avatar character performing choreography in 3D                          |
| Purpose   | Creates an immersive experience by letting users dance with a 3D avatar |
| Platform  | Output is integrated into user-facing camera UI in the app              |

📝 *Used to generate interactive content for “challenge” mode using motion and timeline assets.*


## 📍Features

- Generates **transparent silhouette guide videos** using SAM2 in Google Colab
- Renders **3D avatar choreography** in Unity for immersive dance practice
- Output videos are optimized for overlay in mobile camera view
- Includes `.fbx` and `.mp4` assets for Unity timeline animation
- Sample assets included for testing and prototyping


## 🚀 How to Run (SAM2 module)

This module is designed to run primarily in **Google Colab** using an interactive notebook.  
To generate silhouette guide videos with SAM2:

1. Open the Colab notebook:
    ```bash
    SAM2/extractSillouet.ipynb
    ```

2. Follow the in-notebook steps to:
   - Mount Google Drive  
   - Install dependencies (PyTorch, SAM2)  
   - Download SAM2 checkpoints  
   - Run segmentation and export `.webm` video

📌 For full details, see [`SAM2/README.md`](./SAM2/README.md).


## 🔐 Environment Variables

- No `.env` files are required.
- All configurations are handled directly inside the Colab notebook.
- Video input/output paths are expected to be located in Google Drive.


## 📝 Additional Notes

- The Unity project assumes silhouette and avatar videos share a consistent **resolution and frame rate**.
- Colab-based SAM2 workflow supports both mask propagation and neon visualization.
- `.fbx` files can be added to Unity Timeline for synchronized animation.


## 📦 Sample Assets

| Type           | Location                            |
|----------------|-------------------------------------|
| Sample Video   | `SAM2/SuperShy.mp4`                 |
| Output Video   | `UNITY/processed_videos/challenge_avatar.mp4` |
| Avatar Motion  | `UNITY/suisei_vivideba_motion_.fbx` |
| Colab Notebook | `SAM2/extractSillouet.ipynb`        |
