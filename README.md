# Safety Helmet Detection using YOLOv8

## Project Overview
This computer vision project detects two classes in images:
- With Helmet
- Without Helmet

It uses the YOLOv8n object-detection model.

## Dataset
- Source: Public Roboflow helmet-detection dataset.
- Project dataset: A 250-image subset selected from the source dataset.
- Train: 175 images (70%)
- Validation: 50 images (20%)
- Test: 25 images (10%)
- Labels: YOLO object-detection format.
- Dataset configuration: `dataset_250/data.yaml`

The original public dataset was larger. This project uses a subset for the experiment.
Please consult the original dataset page for attribution and its applicable licence.

## Training Configuration
- Model: YOLOv8n pretrained weights
- Epochs: 30
- Image size: 640
- Batch size: 16
- Environment: Google Colab with NVIDIA T4 GPU

## Held-out Test Results
| Metric | Result |
|---|---:|
| Precision | 83.2% |
| Recall | 82.5% |
| mAP@50 | 84.6% |
| mAP@50–95 | 54.0% |

### Per-class results
| Class | Precision | Recall | mAP@50 | mAP@50–95 |
|---|---:|---:|---:|---:|
| With Helmet | 74.1% | 91.3% | 84.0% | 59.5% |
| Without Helmet | 92.3% | 73.7% | 85.2% | 48.6% |

Metrics are from the 25-image test split; results may vary with a different dataset.

## Main Artifacts
- `dataset_250/` — selected dataset and YOLO labels
- `runs/helmet_250images/weights/best.pt` — best trained model
- `runs/helmet_250images/weights/last.pt` — final-epoch weights, if retained
- `runs/helmet_250images/` — training results and plots
- `evaluation/helmet_250_test/` — test evaluation outputs
- `predictions/helmet_250_predictions/` — prediction images
- `error_analysis/` — test review notes/CSV
- `Final_Helmet_Detection_Report.pdf` — final report

## Running Inference
Install Ultralytics in a Python environment:
```bash
pip install ultralytics
```

Example:
```python
from ultralytics import YOLO

model = YOLO("runs/helmet_250images/weights/best.pt")
results = model.predict(source="path/to/image.jpg", conf=0.25, save=True)
```

Update the model and image paths to match your local setup.

## Error Analysis and Limitations
Ten test examples were visually reviewed during the project, and no obvious errors were noticed in those examples. This does not establish that all predictions are correct. The test set is small, and further review of low-confidence detections, missed objects, occlusion, lighting, and varied camera angles is recommended.

## Future Improvements
- Review and verify annotations across at least 100 images.
- Analyse at least 10 genuinely weak or incorrect predictions and document the actual cases.
- Increase dataset diversity and size.
- Tune confidence thresholds and compare model variants.
- Evaluate on additional real-world images.

## LinkedIn-Ready Summary
Built a Safety Helmet Detection prototype using YOLOv8n and a 250-image dataset subset. Trained for 30 epochs on Google Colab and evaluated on a held-out test split, achieving 84.6% mAP@50. The project includes dataset preparation, model training, evaluation, and prediction visualisations. This is an experimental prototype, not a certified workplace-safety system.
