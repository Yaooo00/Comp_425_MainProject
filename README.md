# Comp_425_MainProject
Based on OpenMMLab's mmdetection3d framework, this project implements a 3D vehicle detection system that integrates MVX-Net (Multimodal Network) and PointPillars. The project utilizes images, point clouds, and calibration files from the KITTI dataset to accurately detect and visualize vehicles (as well as targets such as pedestrians).

# Setting Up the Environment
It is recommended that you use Anaconda to build a standalone Python virtual environment. The recommended environment configuration is as follows:

Clone the project code:
git clone https://github.com/open-mmlab/mmdetection3d.git
The remaining steps follow final_code.ipynd

# Data preparation
Use the following data from the KITTI dataset ==> https://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d (Register first)
1. Left color images of object dataset (.png)
2. Velodyne point clouds (.bin)
3. Training labels of object data set (.txt)
4. (.pkl) The information in the pkl file does not need to be modified.

