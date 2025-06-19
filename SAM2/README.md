# SAM2-Based Video Outline Mask Generation & Neon Effect Rendering

This project demonstrates how to use [Meta AI’s SAM2 (Segment Anything Model 2)](https://github.com/facebookresearch/sam2) to generate outline masks for every frame of a video, visualize the outlines with a neon effect, and export the result as a WebM file.
</br>

## 📁 Preparation

### 1. Download the sample files

Download the following three items in advance:

- `SuperShy.mp4`
- `SuperShy_frames/` (folder of extracted JPEG frames) -> [Download Dataset (Google Drive)](https://drive.google.com/file/d/1ALwWEgiPRNNtJQ-_ALMRXXY0RtmFZNyR/view?usp=drive_link)
- `extractSillouet.ipynb` (Colab notebook)

### 2. Set up Google Drive

Create a folder named `capston` under **MyDrive** and place all three items inside:

MyDrive/  </br>

└── capston/ </br>

├── SuperShy.mp4 </br>

├── extractSillouet.ipynb </br>

└── SuperShy_frames/ </br>

</br>

## ⚙️ Colab Environment

### 3. Select a GPU runtime

- Open **Runtime → Change runtime type** and choose any **GPU**.

### 4. Install required system libraries and Python packages

```python
!apt-get -qq install -y libsm6 libxext6 && pip install -q -U opencv-python
```

## 5. 5. Mount Google Drive

```python
from google.colab import drive
drive.mount('/content/drive')
```

</br>

## 🔧 Install SAM2 and Download Checkpoints

```python
!git clone https://github.com/facebookresearch/sam2.git
%cd sam2
!pip install -e .
%cd checkpoints
! ./download_ckpts.sh
%cd ..
```

</br>

## 🧠 Model Initialization & Device Selection

```python
from sam2.build_sam import build_sam2_video_predictor

sam2_checkpoint = "./checkpoints/sam2.1_hiera_large.pt"
model_cfg = "configs/sam2.1/sam2.1_hiera_l.yaml"
predictor = build_sam2_video_predictor(model_cfg, sam2_checkpoint, device=device)
```

</br>

## 📷 Load the Video & Prepare Frame List

```python
video_dir = "/content/drive/MyDrive/capston/SuperShy_frames"
frame_names = sorted([...])  # sort JPG frame names numerically
```

</br>

## 🖱️ User Point-Click Annotation

- For each body part (full body, arms, legs, head), prepare an array of points and label values.
- Call predictor.add_new_points_or_box() to create the initial mask for each object.


</br>

## 🔁 Propagate Masks to All Frames

```python
video_segments = {}
for out_frame_idx, out_obj_ids, out_mask_logits in predictor.propagate_in_video(inference_state):
    ...
```

</br>

## 🧪 Visualize Masks & Save the Result

- Convert each mask to an outline.
- Apply a neon effect.
- Save frames as RGBA PNG images.
- Stitch frames into a WebM file.

```python
!ffmpeg -framerate 30 \
  -i "/content/drive/MyDrive/capston/frames_rgba/frame_%05d.png" \
  -c:v libvpx -pix_fmt yuva420p -auto-alt-ref 0 \
  -b:v 4M -metadata:s:v:0 alpha_mode="1" \
  "/content/drive/MyDrive/capston/SuperShy_contour.webm"

# Remove black background (chromakey)
!ffmpeg -i "/content/drive/MyDrive/capston/SuperShy_contour.webm" \
-vf "chromakey=0x000000:0.10:0.00,format=yuva420p" \
-c:v libvpx \
-pix_fmt yuva420p \
-auto-alt-ref 0 \
-b:v 4M \
"/content/drive/MyDrive/capston/SuperShy_contour_alpha.webm"
```

</br>

## 🧾 Notes

- Point coordinates can be clicked manually or loaded from a predefined file.
- The dictionary video_segments can be saved to video_segments.pkl and re-loaded later.
- The final output SuperShy_contour_alpha.webm is a transparent WebM file containing only neon outlines.



</br>

## 📎 Dependencies

- `torch`
- `torchvision`
- `opencv-python`
- `matplotlib`
- `Pillow`
- `numpy`
