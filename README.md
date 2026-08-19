# OYOUN AL-SAUDIA

## 👥 Team Members

- Majdoleen Alhamdan
- Dana Mosa Alsaidan
- Deema Alaowairdhi
- Haya AbdulMajeed Aljuraysi
- Farah Alqahtani
- Waad Mohammed Alsaif

---

## 📌 Project Description

**OYOUN AL-SAUDIA** is an AI-powered computer vision project that helps tourists recognize famous landmarks in Saudi Arabia from images and receive useful information about them in both **Arabic and English**.

The system is designed as a **single-model computer vision application** for landmark recognition, supported by a secondary video analytics module for counting visitors near landmarks.

The project was developed as a Capstone Project for the **Computer Vision for Developers with Ultralytics** training program delivered by **SDAIA Academy**.

---

## 🎯 Problem Statement

Tourists may visit cultural, historical, and modern landmarks without having immediate access to useful information about the place they are seeing.

OYOUN AL-SAUDIA solves this problem by allowing a tourist to upload or capture an image of a Saudi landmark. The system recognizes the landmark and returns:

- Landmark name
- Prediction confidence
- Arabic description
- English description

The system also includes a secondary video analytics feature that counts visitor movement near a landmark.

---

## 💡 Project Idea

The user provides an image of a Saudi landmark.

The system then:

1. Receives the image.
2. Processes it using a fine-tuned YOLO classification model.
3. Predicts the landmark class.
4. Calculates the prediction confidence.
5. Applies a confidence threshold.
6. Displays the landmark name.
7. Provides tourist information in Arabic and English.

A secondary video module uses YOLO detection and Ultralytics `ObjectCounter` to count people crossing a defined area near a landmark.

---

## 📌 Project Scope

The current scope includes:

- Saudi landmark image classification.
- Recognition of 16 landmark classes.
- Arabic and English landmark information.
- Confidence-based prediction filtering.
- Validation and test evaluation.
- Confusion matrix analysis.
- Real image inference.
- Visitor footfall counting from video.
- ONNX model export.
- Gradio web interface.

The system currently recognizes only the landmarks included in the training dataset.

---

## 🧠 System Architecture

OYOUN AL-SAUDIA uses a **single-model architecture** for the main landmark-recognition task.

### Landmark Recognition Architecture

```text
User Image
    ↓
Image Preprocessing
    ↓
Fine-Tuned YOLO Classification Model
    ↓
Predicted Landmark + Confidence Score
    ↓
Confidence Threshold Check
    ↓
Bilingual Landmark Knowledge Base
    ↓
Arabic + English Tourist Information
```

### Video Analytics Architecture

```text
Input Video
    ↓
YOLO Person Detection
    ↓
Object Tracking
    ↓
Ultralytics ObjectCounter
    ↓
IN / OUT Visitor Count
    ↓
Processed Output Video
```

---

## 🧩 Key Components

### 1. Landmark Classification Model

The main task is **image classification**.

The model is initialized from:

```python
YOLO("yolov8n-cls.pt")
```

It is then fine-tuned on a custom dataset of Saudi landmarks.

### 2. Bilingual Landmark Knowledge Base

Each supported landmark is mapped to:

- Arabic name
- English name
- Arabic description
- English description

### 3. Confidence Threshold

A confidence threshold is used during inference.

If the confidence is below the selected threshold, the system does not confidently announce the landmark and asks the user to try another image, angle, or lighting condition.

### 4. Visitor Footfall Counter

A secondary module uses:

```python
yolov8n.pt
```

with:

```python
ultralytics.solutions.ObjectCounter
```

to detect and count visitors crossing a defined region in a video.

### 5. Deployment

The final classifier can be:

- Exported to ONNX.
- Used through a Gradio web interface.

---

## 🕌 Supported Landmarks

The dataset contains 16 Saudi landmark classes:

1. Diriyah
2. Hegra
3. Ithra
4. Maraya
5. Al Faisaliah Tower
6. Al Masmak Palace
7. Al Rahmah Mosque
8. Ibrahim Palace
9. Jabal AlFil (Elephant Rock)
10. King Abdullah Financial District (KAFD)
11. Kingdom Tower
12. Nassif House Museum
13. Quba Mosque
14. Riyadh Water Tower
15. The Clock Towers
16. The Kaaba

---

## 📊 Dataset

The dataset contains approximately 400 images distributed across 16 Saudi landmark classes.

### Dataset Source

Add the exact source before final submission:

```text
Dataset source: <Kaggle / manually collected images / own images / other source>
```

### Raw Dataset Structure

```text
Data/
├── Diriyah/
├── Hegra/
├── Ithra/
├── Maraya/
└── ...
```

### Train / Validation / Test Structure

```text
dataset/
├── train/
│   ├── Diriyah/
│   ├── Hegra/
│   └── ...
├── val/
│   ├── Diriyah/
│   ├── Hegra/
│   └── ...
└── test/
    ├── Diriyah/
    ├── Hegra/
    └── ...
```

---

## 🔎 Dataset Exploration

Before training, the notebook:

- Detects the available classes.
- Counts images per class.
- Visualizes class distribution.
- Displays random samples.
- Checks dataset structure.
- Splits the data into training, validation, and test sets.

---

## 🚀 Model Training

The project uses **transfer learning** with a pretrained YOLO classification model.

Example configuration:

```python
model = YOLO("yolov8n-cls.pt")

train_results = model.train(
    data=SPLIT_DIR,
    epochs=40,
    imgsz=224,
    batch=16,
    patience=10,
    augment=True,
    degrees=10,
    fliplr=0.5,
    hsv_h=0.015,
    hsv_s=0.4,
    hsv_v=0.4
)
```

### Training Configuration

- Base model: `yolov8n-cls.pt`
- Image size: `224px`
- Maximum epochs: `40`
- Batch size: `16`
- Early stopping patience: `10`
- Transfer learning: Enabled
- Data augmentation: Enabled

### Data Augmentation

The project uses:

- Rotation
- Horizontal flipping
- HSV color augmentation

---

## 📈 Model Evaluation

The trained model is evaluated using:

- Validation Top-1 Accuracy
- Validation Top-5 Accuracy
- Test Top-1 Accuracy
- Test Top-5 Accuracy
- Confusion Matrix
- Confidence analysis

### Final Results

Update these values after final training:

| Metric                        | Result |
| ----------------------------- | ------ |
| Validation Top-1 Accuracy     | TBD    |
| Validation Top-5 Accuracy     | TBD    |
| Test Top-1 Accuracy           | TBD    |
| Test Top-5 Accuracy           | TBD    |
| Selected Confidence Threshold | TBD    |

### Confusion Matrix Interpretation

After final evaluation, document:

- Which classes were predicted correctly most often.
- Which landmarks were confused with each other.
- Possible reasons for confusion.
- Whether visual similarity, lighting, image angle, or limited samples affected performance.

Example:

```text
The model performed well across most landmark classes.
Some visually similar landmarks showed minor confusion due to similar
architectural features, image angles, lighting conditions, or limited samples.
```

---

## 🔍 Real Inference

The project tests the trained model on unseen images.

```text
New Tourist Image
      ↓
YOLO Classification
      ↓
Top Prediction
      ↓
Confidence Score
      ↓
Threshold Check
      ↓
Landmark Information
```

The expected result contains:

- Predicted landmark
- Prediction confidence
- Arabic landmark name
- English landmark name
- Arabic description
- English description

---

## 🌍 Bilingual Tourist Information

Example output:

```text
EN | Kingdom Tower
Confidence: 94%
Kingdom Tower is one of Riyadh's most recognizable landmarks...

AR | برج المملكة
الثقة: 94%
يعد برج المملكة من أبرز معالم مدينة الرياض...
```

---

## 👥 Visitor Footfall Analytics

The secondary video analytics module:

- Opens a real video.
- Detects people.
- Tracks movement.
- Counts people crossing a defined line.
- Calculates IN and OUT counts.
- Saves the processed video.

Possible use cases:

- Tourist attractions
- Museums
- Heritage sites
- Events
- Visitor-flow analytics

---

## 📦 Model Export

The final model is exported to ONNX:

```python
export_path = model.export(format="onnx")
```

ONNX provides a portable format suitable for lightweight CPU inference and future integration with other applications.

---

## 🌐 Gradio Deployment

The project includes a Gradio demo.

The user can:

1. Upload or capture an image.
2. Run landmark recognition.
3. View the predicted landmark.
4. View the confidence score.
5. Read Arabic and English tourist information.

---

## ⚙️ Prerequisites

Recommended environment:

- Python 3.x
- Google Colab
- GPU runtime recommended

Main libraries:

- ultralytics
- gradio
- opencv-python
- matplotlib
- Pillow
- numpy
- arabic-reshaper
- python-bidi
- onnx
- onnxruntime

---

## 🔐 API Keys and Environment Variables

The current project does **not require external API keys** for its core functionality.

If future versions use external APIs, maps, LLM services, or tourism platforms:

- Store API keys in environment variables.
- Never commit secrets to GitHub.
- Use a `.env` file locally.
- Add `.env` to `.gitignore`.

Example:

```text
API_KEY=your_key_here
```

---

## 🖥️ How to Run

### 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

### 2. Install Dependencies

If a `requirements.txt` file is available:

```bash
pip install -r requirements.txt
```

Or install the main dependencies directly:

```bash
pip install ultralytics gradio arabic-reshaper python-bidi onnx onnxruntime
```

### 3. Open the Notebook

Open:

```text
SaudiVision_Guide_Capstone_Aligned.ipynb
```

in Google Colab.

### 4. Enable GPU

In Google Colab:

```text
Runtime → Change runtime type → GPU
```

A T4 GPU is recommended when available.

### 5. Upload the Dataset

Upload the dataset ZIP when requested.

Expected structure:

```text
Data/<landmark_name>/*.jpg
```

or:

```text
Data/<landmark_name>/*.png
```

### 6. Run the Notebook

Run all cells from top to bottom.

### 7. Review Evaluation Results

Record:

- Validation Top-1 Accuracy
- Validation Top-5 Accuracy
- Test Top-1 Accuracy
- Test Top-5 Accuracy
- Confusion Matrix
- Confidence Threshold

### 8. Test a New Image

Upload an unseen image and run the inference section.

### 9. Run Video Analytics

Upload a short `.mp4` video containing people near a landmark.

### 10. Export the Model

Run the ONNX export section.

### 11. Launch Gradio

Run the Gradio deployment cell and open the generated URL.

---

## ✅ Expected Output

### Image Classification Output

- Predicted landmark
- Confidence score
- Arabic landmark name
- English landmark name
- Arabic description
- English description

### Video Analytics Output

- Processed video
- People IN count
- People OUT count
- Total visitor count

---

## 📝 Technical Documentation

This README provides the technical documentation required for the project.

It documents:

- Project objective
- Problem statement
- System scope
- Architecture
- Main components
- Dataset structure
- Training configuration
- Evaluation methodology
- Confidence threshold
- Real inference
- Video analytics
- Deployment
- Required setup
- Expected output
- Limitations
- Future improvements

The notebook contains the executable implementation, while this README provides the full technical overview from the GitHub repository landing page.

---

## 🔀 Git Version-Control Practices

The repository should be updated continuously using meaningful, incremental commits instead of one final bulk upload.

Recommended commit examples:

```text
Initial project setup
Add dataset exploration
Add train validation test split
Add YOLO landmark classification training
Add validation and test evaluation
Add confusion matrix analysis
Add bilingual landmark inference
Add visitor footfall counter
Add ONNX export
Add Gradio deployment
Update README documentation
```

A good Git history should show the project evolving over time.

---

## 🙈 Recommended .gitignore

Create a `.gitignore` file in the repository and add:

```gitignore
# Python
__pycache__/
*.pyc
*.pyo

# Environment variables and secrets
.env
.env.*
*.key

# Jupyter
.ipynb_checkpoints/

# Generated training outputs
runs/
results/

# Model files
*.pt
*.onnx

# Temporary files
*.tmp
*.log

# Operating system files
.DS_Store
Thumbs.db
```

If the final trained model is required for submission, upload only the required final artifact or provide a documented download location.

---

## ⚠️ Limitations

Current limitations include:

- Relatively small dataset.
- Recognition is limited to the 16 trained landmark classes.
- Similar-looking landmarks may be confused.
- Performance can decrease with poor lighting.
- Unusual camera angles can affect predictions.
- Occlusion can affect recognition.
- Low-resolution images can reduce accuracy.
- Landmark descriptions should be fact-checked before real-world deployment.
- Visitor counting may be affected by crowd overlap and occlusion.

---

## 💡 Future Improvements

Future improvements may include:

- Adding more Saudi landmarks.
- Expanding to international landmarks.
- Increasing images per class.
- Improving dataset diversity.
- Testing larger YOLO classification models.
- GPS integration.
- Nearby attraction recommendations.
- Maps and navigation.
- Real-time camera recognition.
- Mobile application deployment.
- Larger tourism knowledge base.
- More languages.

---

## 🎓 Training Program Attribution

This project was completed as the Capstone Project for:

**Computer Vision for Developers with Ultralytics**

Delivered by:

**SDAIA Academy**

Cohort / Session dates:

```text
<ADD YOUR COHORT OR SESSION DATES HERE>
```

SDAIA Academy GitHub:

https://github.com/SDAIAAcademy

---

## ✅ GitHub Submission Requirements Covered

This README includes the required GitHub submission elements:

- Clear and comprehensive project description.
- Professional README visible from the repository landing page.
- Problem statement and project scope.
- System architecture overview.
- Key components and technical configuration.
- Prerequisites and setup instructions.
- How to run and use the project.
- Expected output.
- API key and environment-variable guidance.
- Dataset documentation.
- Training and evaluation documentation.
- Deployment documentation.
- Git version-control guidance.
- Meaningful commit-message examples.
- `.gitignore` guidance for secrets and generated files.
- Training program attribution.
- SDAIA Academy GitHub reference.
- Team member names.

---

## ✅ Final Submission Checklist

Before final submission, confirm:

- [ ] Every trainee has an active GitHub account.
- [ ] The project is published on GitHub.
- [ ] The repository is accessible as required.
- [ ] The README is visible from the repository landing page.
- [ ] The project description is complete.
- [ ] The architecture is documented.
- [ ] The dataset source is documented.
- [ ] Final training results are added.
- [ ] Validation and test results are added.
- [ ] Confusion matrix interpretation is completed.
- [ ] The notebook runs from top to bottom.
- [ ] Installation and setup instructions are correct.
- [ ] No API keys or secrets are committed.
- [ ] `.gitignore` is included in the repository.
- [ ] Git commit history is incremental and meaningful.
- [ ] Training program name is included.
- [ ] Cohort/session dates are included.
- [ ] SDAIA Academy GitHub link is included.
- [ ] All team members are listed.
