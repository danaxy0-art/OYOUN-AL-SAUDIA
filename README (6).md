# عيون السعودية | OYOUN AL-SAUDIA

A tourist points a camera at any Saudi landmark, and the app instantly recognizes it and shows information about it in **Arabic and English**.

Built for the **Computer Vision for Developers with Ultralytics** capstone — **SDAIA Academy**, delivered via Learning Space.
<!-- EDIT ME: add your cohort/session dates, e.g. "Cohort: March 2026" -->

Reference: [SDAIA Academy on GitHub](https://github.com/SDAIAAcademy)

## Team

**OYOUN AL-SAUDIA**

- Majdoleen Alhamdan
- Dana Mosa Alsaidan
- Deema Alaowairdhi
- Haya AbdulMajeed Aljuraysi
- Farah Alqahtani
- Waad Mohammed Alsaif

## What it does

| # | Deliverable | Where in the notebook |
|---|---|---|
| 1 | Core vision task & inference | Sections 5 & 7 — `yolov8n-cls.pt` fine-tuned classifier, real `model.predict` inference |
| 2 | Real-world solution & video analytics | Section 8 — `ultralytics.solutions.ObjectCounter` counts visitors crossing a line in landmark footage |
| 3 | Model evaluation | Section 6 — `model.val`, top-1/top-5 accuracy, confusion matrix, interpretation |
| 4 | Custom data & training | Section 5 — `model.train` fine-tuned on a self-collected 16-class Saudi landmark dataset |
| 5 | Deployment & export | Sections 9–10 — ONNX export + bilingual Gradio app |
| 6 | Documentation & evidence | This README + executed notebook with captured outputs |

**Landmarks recognized (16 classes):** Diriyah, Hegra, Ithra, Maraya, Al Faisaliah Tower, Al Masmak Palace, Al Rahmah Mosque, Ibrahim Palace, Jabal AlFil (Elephant Rock), King Abdullah Financial District, Kingdom Tower, Nassif House Museum, Quba Mosque, Riyadh Water Tower, The Clock Towers, The Kaaba.

## How it works

- **Model:** `yolov8n-cls.pt` fine-tuned on a custom 16-class dataset (399 images total, 80/20 train/val split → 321 train / 78 val).
- **Training:** 40 epochs, imgsz 224, batch 16, early-stopping patience 10, with rotation/flip/HSV color augmentation.
- **Result:** 97.4% top-1 / 100% top-5 accuracy on the validation set.
- **Video analytics:** a separate `ultralytics.solutions.ObjectCounter` pipeline (pretrained `yolov8n.pt`, person class) tracks and counts people crossing a line in front of a landmark, for tourism-board-style foot-traffic numbers.
- **Deployment:** the classifier is exported to ONNX for lightweight CPU inference, and served through a bilingual Gradio web app.

## Prerequisites

- Google Colab (GPU runtime recommended — T4 or better) or a local Python 3.10+ environment with a CUDA GPU.
- Your own `archive.zip` of landmark photos, laid out as `Data/<landmark name>/*.jpg`.
- A short `.mp4`/`.mov` clip of people walking in front of a landmark, for the visitor-counter section (optional).

## Setup & run

1. Open `OYOUN_AL_SAUDIA.ipynb` in Google Colab.
2. `Runtime → Change runtime type → GPU`.
3. Run the cells top to bottom.
4. When prompted, upload `archive.zip` (Section 2).
5. In Section 8, upload a short video clip if you want to try the visitor counter.
6. Section 10 launches the Gradio demo — open the printed public URL to try the bilingual identifier.

## Dataset

16 Saudi landmarks, 399 images total (19–30 per class), collected from public online sources (one search per landmark) rather than personally photographed. `runs/`, weights, and the raw `Data/`/`archive.zip` are excluded from the repo — see `.gitignore`.

## Repo structure

```
OYOUN_AL_SAUDIA.ipynb   # end-to-end capstone notebook (all 6 deliverables)
README.md
.gitignore              # excludes datasets, weights, and generated runs/
```

`runs/`, exported weights (`*.onnx`, `*.pt`), and the raw dataset are intentionally **not** committed — see `.gitignore`. Anyone cloning the repo regenerates them by running the notebook with their own `archive.zip`.

## Attribution

This project — **OYOUN AL-SAUDIA** (Majdoleen Alhamdan, Dana Mosa Alsaidan, Deema Alaowairdhi, Haya AbdulMajeed Aljuraysi, Farah Alqahtani, Waad Mohammed Alsaif) — was completed as the capstone for **Computer Vision for Developers with Ultralytics**, delivered by **SDAIA Academy** via Learning Space.
<!-- EDIT ME: cohort/session dates go here too if not added above -->
