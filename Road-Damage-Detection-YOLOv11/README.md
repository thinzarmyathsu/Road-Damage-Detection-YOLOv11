# Road Damage Detection — YOLOv11

A computer vision coursework project exploring **YOLO11n (YOLOv11)** object detection for five types of road damage. This repository presents **my learning-rate experiments** from a larger group project.

## Objective
Detect road defects from images and compare the impact of initial learning rate on detection performance.

## Classes
1. Longitudinal crack
2. Transverse crack
3. Alligator crack
4. Other corruption
5. Pothole

## Technologies
Python, Ultralytics YOLO11n, PyTorch, OpenCV, pandas, Matplotlib, and Jupyter Notebook.

## My contribution
I conducted the **learning-rate comparison**, preparing the training notebook, running three training configurations and evaluating the saved models on the test subset. The broader road-damage project involved other team members; this repository covers the portion in the attached submission.

## Training configuration
- Base model: `yolo11n.pt`
- Initial learning rates compared: **0.0001**, **0.001**, **0.01**
- Optimizer: SGD
- Epochs requested: 50; early-stopping patience: 20
- Image size: 640
- Batch size: 16
- Data augmentation enabled
- Notebook creates class-balanced subsets from an existing train/validation/test dataset directory.

## Recorded test results
These values were extracted from the **saved notebook's test-output cells**, not independently reproduced in this repository. The outputs were removed from the public notebook to avoid publishing local filesystem paths and bulky logs.

| Initial learning rate | mAP@50 | mAP@50–95 | Precision | Recall |
|---:|---:|---:|---:|---:|
| 0.0001 | 0.2456 | 0.1078 | 0.3225 | 0.3022 |
| 0.001 | 0.4535 | 0.2181 | **0.5297** | 0.4547 |
| **0.01** | **0.4701** | **0.2204** | 0.5247 | **0.4744** |

**Interpretation:** Of these three saved runs, learning rate **0.01** achieved the highest test mAP@50 and mAP@50–95, while **0.001** had slightly higher precision. These figures describe these particular experiments, not guaranteed performance on other roads or datasets.

## Repository structure
```text
notebooks/learning_rate_experiments.ipynb  # Training, evaluation and camera demo code
models/lr_0.0001_best.pt              # Saved model weights
models/lr_0.001_best.pt
models/lr_0.01_best.pt
requirements.txt
.gitignore
```

## How to run
1. Install Python and the dependencies with `pip install -r requirements.txt`.
2. Obtain a compatible YOLO-labelled road-damage dataset, using the appropriate source and permissions. **Dataset files are not included** in this repository.
3. Organize your dataset into `train/images`, `train/labels`, `val/images`, `val/labels`, `test/images`, and `test/labels` under one directory.
4. Set the environment variable `RDD_DATASET_PATH` to the dataset's local directory, or place the dataset in `data/RDD_SPLIT`.
5. Open the notebook and execute the cells in order. Training takes substantial computing resources; a CUDA GPU was used for the original runs.

**Reproducibility note:** The notebook retains the original workflow for reference, including dataset subset construction and experiment paths. The dataset, cached subsets, training-history CSVs, and actual training execution are not included; running it from scratch may require adjusting local paths or folder names. The supplied checkpoints represent archived outputs, and should only be loaded if you trust their origin because PyTorch model loading can involve unsafe deserialization.

## Project status
Academic portfolio demonstration. Not a production road inspection or safety system.
