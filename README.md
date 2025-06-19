# DANZLE-Assets
Danzle 프로젝트에서 활용되는 SAM2 기반 실루엣 영상과 Unity 연동 자료를 포함한 전처리 리소스 레포지토리입니다.


# Danzle-Assets

## 💡 Project Purpose

This repository contains **preprocessing assets** and **helper scripts** used in the Danzle project. It includes two major components:

- SAM2-based **silhouette video generation**
- Unity-based **avatar choreography video production**
- Sample data and usage examples for precomputed media

These assets are **not part of the live backend/frontend runtime**, but are essential during development or content preparation.

---

## 📁 Directory Structure

Danzle-assets/
├── SAM2/ # Silhouette video generation tool
│ ├── sam2_generate.py # PyTorch-based script (requires GPU)
│ ├── requirements.txt
│ └── sample_input/ # Sample dance images or video frames
│
├── UNITY/ # Processed files for Unity consumption
│ ├── processed_videos/ # .mp4 silhouette videos with transparency
│ └── conversion_tool/ # (Optional) ffmpeg or post-processing scripts
│
└── README.md



## SAM2 Tech Stacks

| Component          | Technologies / Notes                      |
| ------------------ | ----------------------------------------- |
| Segmentation Model | SAM2 (Segment Anything Model 2)           |
| Framework          | PyTorch                                   |
| Input Format       | Image or video (frame-by-frame)           |
| Output             | Binary silhouette masks, silhouette video |
| Environment        | GPU recommended (CUDA support)            |


## Unity Tech Stacks

| Component | Technologies                    |
| --------- | ------------------------------- |
| Engine    | Unity 2022.3 LTS                |
| Output    | MP4 guide video                 |
| Purpose   | Avatar-based choreography guide |




















