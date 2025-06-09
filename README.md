import zipfile
from pathlib import Path

# Create project folder and files
project_path = Path("/mnt/data/yolov5_project")
project_path.mkdir(exist_ok=True)

# 1. README.md
readme = """# YOLOv5 Object Detection Project

This project uses YOLOv5 for real-time object detection. It includes setup files, sample annotations, and an inference script.

## How to Use

1. Clone YOLOv5 from [Ultralytics GitHub](https://github.com/ultralytics/yolov5).
2. Copy these config and label files into your yolov5 folder.
3. Use `run_yolov5.py` to perform inference.
"""

(project_path / "README.md").write_text(readme)

# 2. data.yaml
data_yaml = """train: data/images/train
val: data/images/val

nc: 1
names: ['animal']
"""
(project_path / "data.yaml").write_text(data_yaml)

# 3. image1.txt
image_txt = "0 0.512 0.634 0.245 0.312\n"
(project_path / "image1.txt").write_text(image_txt)

# 4. run_yolov5.py
run_code = """# YOLOv5 Inference Script

import torch

# Load model
model = torch.hub.load('ultralytics/yolov5', 'yolov5s', pretrained=True)

# Inference on an image
results = model('data/images/test.jpg')  # Replace with your image path

# Display results
results.print()
results.show()
"""
(project_path / "run_yolov5.py").write_text(run_code)

# 5. .gitignore
gitignore = """*.pt
*.jpg
*.png
runs/
__pycache__/
.ipynb_checkpoints/
"""
(project_path / ".gitignore").write_text(gitignore)

# Create ZIP file
zip_path = "/mnt/data/yolov5_project_bundle.zip"
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for file in project_path.glob("*"):
        zipf.write(file, arcname=file.name)

zip_path
