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
data/kitti/
├── training/

│   ├── image_2/       # Left color images (e.g., 000000.png, 000001.png, …)

│   ├── velodyne/      # Velodyne point clouds (e.g., 000000.bin, 000001.bin, …)

│   ├── calib/         # Calibration files (e.g., 000000.txt or converted 000000.pkl)

│   └── label_2/       # Object annotation files (e.g., 000000.txt, 000001.txt, …)

└── ImageSets/         # Data split files

    ├── train.txt    # e.g., sample IDs 000000 ~ 000035 (36 samples)
    
    ├── val.txt      # e.g., sample IDs 000036 ~ 000039 (4 samples)
    
    └── test.txt     # e.g., sample IDs 000040 ~ 000049 (10 samples)

# Generate Data Index
After preparing the data, run the following command to generate KITTI information files (in .pkl format) for subsequent training and testing:



# IMPORTANT NOTE: 
1. To ensure that MVX-Net can be loaded and visualized correctly, the following code needs to be added at the top of this configuration file:


import os
os.environ['DISPLAY'] = '1'


2. As mentioned in the REPORT, data consistency is important. Since the calibration files are internally numbered (000008), make sure that the numbering of the image, point cloud and calibration files is consistent. If using new data, rename all relevant files to the same number (e.g. 000008.xxx).


# Activate MVX-Net (Final Step)
python demo/multi_modality_demo.py demo/data/kitti/000008.bin demo/data/kitti/000008.png demo/data/kitti/000008.pkl configs/mvxnet/mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class.py "D:\1.Concordia University\2025 Winter\COMP 425\Project\mvxnet_fpn_dv_second_secfpn_8xb2-80e_kitti-3d-3class-8963258a.pth" --show --out-dir outputs\multi_modality_results --print-result
# Activate PointPillars (Final Step)
python demo/pcd_demo.py demo/data/kitti/000008.bin pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth --show
