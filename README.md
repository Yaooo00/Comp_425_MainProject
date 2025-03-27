# Comp_425_MainProject
This project implements a 3D vehicle detection system based on OpenMMLab's mmdetection3d framework. It leverages both MVX-Net (a multimodal network that fuses RGB images with LiDAR point clouds) and PointPillars (which converts point cloud data into pseudo-images for efficient detection) to accurately detect and visualize vehicles, as well as other targets such as pedestrians and cyclists. In addition, the project compares the performance of the two methods to provide insights for subsequent development.

# Setting Up the Environment
It is recommended that you use Anaconda to build a standalone Python virtual environment. The recommended environment configuration is as follows:

Python Version: 3.8.20 (default, Oct  3 2024, 15:19:54) [MSC v.1929 64 bit (AMD64)]
PyTorch Version: 1.13.1
CUDA Version: 11.7
CUDA Can Use Or Not: True

1. Clone the project code:
git clone https://github.com/open-mmlab/mmdetection3d.git

2. Install Dependencies:
Please follow the instructions in the final_code.ipynb to install the required packages. Ensure that your Python, PyTorch, mmcv, mmengine, and other dependencies meet the version requirements.

# Data preparation
Use the following data from the KITTI dataset ==> https://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d (Register first)
1. Left color images of object dataset (.png)
2. Velodyne point clouds (.bin)
3. Training labels of object data set (.txt)
4. (.pkl) The information in the pkl file does not need to be modified.

# Data Directory Structure
Ensure that your data is organized under the data/kitti directory as follows (You need to add these files to it yourself)
![image](https://github.com/user-attachments/assets/7393c9fb-980d-4e13-bd25-da2c9f5bb065)


# Generate Data Index
After preparing the data, run the following command to generate KITTI information files (in .pkl format) for subsequent training and testing:

python tools/create_data.py kitti --root-path data/kitti --out-dir data/kitti --extra-tag kitti

# Train 
1.  Training PointPillars
To train PointPillars, use the corresponding configuration file:

python tools/train.py pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py

2.  Training MVX-Net
To train MVX-Net, use a configuration file such as:

python tools/train.py configs/mvxnet/mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class.py

# Testing & Evaluation
1. Testing PointPillars
Since PointPillars is a LiDAR-only method, use the following command (with --task lidar_det):

python tools/test.py configs/pointpillars/pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py "hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth" --task lidar_det --show

  
2. 4.2 Testing MVX-Net
For MVX-Net, which fuses image and point cloud data, the recommended test command is:

python tools/test.py configs/mvxnet/mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class.py "D:\1.Concordia University\2025 Winter\COMP 425\Project\mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class-8963258a.pth" --task lidar_det --show --out-dir outputs\multi_modality_results --print-result


# Visualization
IMPORTANT NOTE for Visualization:
To ensure loads and visualizes correctly, add the following code at the top of demo/multi_modality_demo.py and demo/pcd_demo.py:

import os

os.environ['DISPLAY'] = '1'

In treminal you should install mmdet3d   --> pip install -e .


1. MVX-Net Visualization
To visualize the multimodal detection results (fusing image and point cloud), run:

python demo/multi_modality_demo.py demo/data/kitti/000008.bin demo/data/kitti/000008.png demo/data/kitti/000008.pkl configs/mvxnet/mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class.py "D:\1.Concordia University\2025 Winter\COMP 425\Project\mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class-8963258a.pth" --show --out-dir outputs\multi_modality_results --print-result
![image](https://github.com/user-attachments/assets/4fa54b37-5c05-496f-8ccb-f5fc2efbf813)

2. PointPillars Visualization
To visualize PointPillars' detection results on point cloud data, run:
python demo/pcd_demo.py demo/data/kitti/000008.bin pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py "hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth" --show
![image](https://github.com/user-attachments/assets/d88fe351-8e26-4c73-aab0-a4b119b6f000)

NOTE: Data consistency is critical in the visualization section. Ensure that the image, point cloud, calibration files, and annotation files are numbered consistently. If using new data, rename all corresponding files to the same format (e.g. 000008.xxx).
