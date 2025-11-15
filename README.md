# Space Station Safety Equipment Detection
colab link : https://drive.google.com/drive/u/0/folders/1n7s2mE3dAYCVmvr_U8xqfcI-IbCDz6f9
This project implements a YOLO-based object detection system for identifying 7 critical safety equipment items in a space station environment as part of the Duality AI Space Station Challenge #2.

## Object Classes
1. OxygenTank
2. NitrogenTank
3. FirstAidBox
4. FireAlarm
5. SafetySwitchPanel
6. EmergencyPhone
7. FireExtinguisher

## Prerequisites

### Hardware Requirements
- Minimum 8GB RAM (16GB recommended)
- GPU recommended but not required (CPU support available)

### Software Requirements
- Windows 10/11 or compatible OS
- Anaconda/Miniconda
- Python 3.8 or higher

## Environment Setup

1. Ensure Anaconda is installed on your system
2. Navigate to the `ENV_SETUP` directory:
   ```bash
   cd ENV_SETUP
   ```
3. Run the setup script:
   ```bash
   setup_env.bat
   ```
4. Activate the environment:
   ```bash
   conda activate EDU
   ```

## Project Structure
```
Hackathon2_scripts/
├── ENV_SETUP/              # Environment setup scripts
├── hackathon2_train_1/     # Training dataset
├── hackathon2_test3/       # Test dataset
├── runs/                   # Training outputs
├── src/                    # Source code
│   ├── detection/          # Object detection modules
│   ├── training/           # Model training modules
│   ├── utils/              # Utility files
│   └── visualization/      # Visualization tools
├── main.py                 # Main entry point
├── yolov8s.pt              # Pre-trained YOLO model
└── README.md               # This file
```

## Usage Instructions

### 1. Training the Model
To train the model with the provided dataset:
```bash
conda activate EDU
python main.py train
```

Training parameters:
- Epochs: 50
- Batch size: 16
- Image size: 640
- Optimizer: AdamW
- Initial learning rate: 0.001

### 2. Running Detection on Images
To detect safety equipment in a single image:
```bash
conda activate EDU
python main.py detect path/to/your/image.jpg
```

### 3. Real-time Camera Detection
To run real-time detection using your webcam:
```bash
conda activate EDU
python main.py camera
```

Controls:
- Press 'q' to quit
- Press 's' to save a screenshot
- Press 'f' to check for model updates

### 4. Mobile Application Interface
To run the mobile application interface:
```bash
conda activate EDU
python main.py mobile
```

Features:
- Real-time camera detection
- Image file processing
- Equipment maintenance information
- Detection history tracking

### 5. Visualization Tools
To visualize training results and predictions:
```bash
conda activate EDU
python main.py visualize
```

## Reproducing Final Results

1. Ensure environment is set up as described above
2. Run the prediction script on the test dataset:
   ```bash
   conda activate EDU
   python src/detection/predict.py
   ```
3. Results will be saved in the `predictions/` directory with:
   - Annotated images in `predictions/images/`
   - Label files in `predictions/labels/`
   - Confusion matrix visualization

## Expected Outputs

### Performance Metrics
After running predictions, you should see metrics similar to:
- mAP@0.5: ~0.267
- Precision: ~0.433
- Recall: ~0.283

### Output Files
1. **Annotated Images**: Images with bounding boxes around detected equipment
2. **Label Files**: Text files in YOLO format containing detection coordinates
3. **Confusion Matrix**: Visualization of model performance across classes

### Directory Structure After Running
```
predictions/
├── images/        # Annotated images with bounding boxes
├── labels/        # Detection labels in YOLO format
└── confusion_matrix.png  # Model performance visualization
```

## Interpreting Results

### Metrics Explanation
- **mAP@0.5**: Mean Average Precision at 50% IoU threshold - higher is better
- **Precision**: Proportion of detections that are correct - higher is better
- **Recall**: Proportion of actual objects that were detected - higher is better

### Class-wise Performance
The model typically performs best on:
1. OxygenTank (highest mAP@0.5)
2. FirstAidBox
3. FireExtinguisher

Performance may be lower for:
1. EmergencyPhone
2. SafetySwitchPanel
3. FireAlarm

## Troubleshooting

### Common Issues
1. **Import Errors**: Ensure all dependencies are installed with `install_packages.bat`
2. **CUDA Errors**: The model will automatically fall back to CPU if GPU is not available
3. **Memory Issues**: Large images are automatically resized to prevent memory overflow
4. **Camera Access**: Ensure no other applications are using the webcam

### Model Loading Issues
If the trained model cannot be found, the system will automatically fall back to the pre-trained yolov8s.pt model.

## Additional Information

### Dataset Information
- Training images: 1216
- Validation images: 304
- Test images: 1408

### Model Information
- Architecture: YOLOv8s
- Input size: 640x640
- Classes: 7 safety equipment items

For more detailed information about the project implementation, refer to `PROJECT_SUMMARY.md`.
