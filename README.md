# YOLOv8 C++ Inference with OpenCV DNN

This example demonstrates how to perform inference using Ultralytics YOLOv8 models in C++ leveraging the [OpenCV DNN module](https://docs.opencv.org/4.x/d6/d0f/group__dnn.html).

## 🛠️ Usage

Follow these steps to set up and run the C++ inference example:

```bash
# 1. Clone the repository
git clone git@github.com:eden-ouob/YOLOv8-CPP-Inference.git
cd YOLOv8-CPP-Inference

# 2. Using a Python virtual environment is highly recommended to avoid dependency conflicts.
python -m venv yolov8
source yolov8/bin/activate

# 3. Install Ultralytics Python package (needed for exporting models)
pip install .

# 4. Export Models: Add yolov8*.onnx and/or yolov5*.onnx models (see export instructions below)
#    Place the generated `.onnx` files (e.g., `yolov8s.onnx`) into the `ultralytics/examples/YOLOv8-CPP-Inference/` directory.
yolo export model=yolov8s.pt imgsz=640,480 format=onnx opset=12 simplify=True device=0 # Example: 640x480 resolution

# 5. Update Source Code: Edit main.cpp and set the 'projectBasePath' variable
#    to the absolute path of the 'YOLOv8-CPP-Inference' directory on your system.
#    Example: std::string projectBasePath = "/path/to/your/ultralytics/examples/YOLOv8-CPP-Inference";

# 6. Configure OpenCV DNN Backend (Optional - CUDA):
#    - The default CMakeLists.txt attempts to use CUDA for GPU acceleration with OpenCV DNN.
#    - If your OpenCV build doesn't support CUDA/cuDNN, or you want CPU inference,
#      remove the CUDA-related lines from CMakeLists.txt.

# 7. Build the project
mkdir build
cd build
cmake ..
make

# 8. Run the inference executable
./Yolov8CPPInference
```

**Example Output:**

_yolov8s.onnx:_

![YOLOv8 ONNX Output](https://user-images.githubusercontent.com/40023722/217356132-a4cecf2e-2729-4acb-b80a-6559022d7707.png)

_best_LPR.onnx:_

![image](https://github.com/user-attachments/assets/ac4ba379-34a7-4675-8e8d-14af0a2ab0cc)


## 📝 Notes
- This repository utilizes the [OpenCV DNN API](https://docs.opencv.org/4.x/d6/d0f/group__dnn.html) to run [ONNX](https://onnx.ai/) exported models of YOLOv5 and Ultralytics YOLOv8.
- The example models are exported with a rectangular resolution (640x480), but the code should handle models exported with different resolutions. Consider using techniques like [letterboxing](https://docs.ultralytics.com/modes/predict/#letterbox) if your input images have different aspect ratios than the model's training resolution, especially for square `imgsz` exports.
