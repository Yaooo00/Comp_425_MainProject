# Comp_425_MainProject
This project implements a 3D vehicle detection system based on OpenMMLab's mmdetection3d framework. It leverages both MVX-Net (a multimodal network that fuses RGB images with LiDAR point clouds) and PointPillars (which converts point cloud data into pseudo-images for efficient detection) to accurately detect and visualize vehicles, as well as other targets such as pedestrians and cyclists. In addition, the project compares the performance of the two methods to provide insights for subsequent development.

# Setting Up the Environment
It is recommended that you use Anaconda to build a standalone Python virtual environment. The recommended environment configuration is as follows:

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
Ensure that your data is organized under the data/kitti directory as follows:
![image](https://github.com/user-attachments/assets/7393c9fb-980d-4e13-bd25-da2c9f5bb065)


# Generate Data Index
After preparing the data, run the following command to generate KITTI information files (in .pkl format) for subsequent training and testing:
python tools/create_data.py kitti --root-path data/kitti --out-dir data/kitti --extra-tag kitti

# Train 
1.  Training PointPillars
