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


# IMPORTANT NOTE: 
1. To ensure that MVX-Net can be loaded and visualized correctly, the following code needs to be added at the top of this configuration file:
import os
os.environ['DISPLAY'] = '1'
2. As mentioned in the REPORT, data consistency is important. Since the calibration files are internally numbered (000008), make sure that the numbering of the image, point cloud and calibration files is consistent. If using new data, rename all relevant files to the same number (e.g. 000008.xxx).


# Activate MVX-Net
python demo/multi_modality_demo.py demo/data/kitti/000008.bin demo/data/kitti/000008.png demo/data/kitti/000008.pkl configs/mvxnet/mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class.py "D:\1.Concordia University\2025 Winter\COMP 425\Project\mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class-8963258a.pth" --show --out-dir outputs\multi_modality_results --print-result
# Activate PointPillars
python demo/pcd_demo.py demo/data/kitti/000008.bin pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth --show
