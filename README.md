<div align="center">
    <h1> 
      <img src="assets/imgs/logo.svg" width="35" height="35" /> SOAR
    </h1>
    </h1>
    <h2>Simultaneous Exploration and Photographing with Heterogeneous UAVs for Fast Autonomous Reconstruction</h2>
    <strong>IROS 2024 Oral</strong>
    <br>
        <a href="https://robotics-star.com/people" target="_blank">Mingjie Zhang</a><sup>1,3,*</sup>,
        <a href="https://chen-albert-feng.github.io/AlbertFeng.github.io" target="_blank">Chen
            Feng</a><sup>2,*</sup>,
        <a href="https://robotics-star.com/people" target="_blank">Zengzhi Li</a><sup>1,4</sup>,
        <a href="https://robotics-star.com/people" target="_blank">Guiyong Zheng</a><sup>1</sup>,
        <a href="https://robotics-star.com/people" target="_blank">Yiming Luo</a><sup>1</sup>,
        <br>
        <a href="https://zdh.ncepu.edu.cn/szdw/fjs/2e5352e61fb648aa890d5aaaf1f1447f.htm" target="_blank">Zhu
            Wang</a><sup>4</sup>,
        <a href="https://facultyprofiles.hkust-gz.edu.cn/faculty-personal-page/ZHOU-Jinni/eejinni"
            target="_blank">Jinni Zhou</a><sup>5</sup>,
        <a href="https://uav.hkust.edu.hk/group" target="_blank">Shaojie Shen</a><sup>2</sup>,
        <a href="https://robotics-star.com/people" target="_blank">Boyu Zhou</a><sup>1,†</sup>
        <p>
        <h45>
            <sup>1</sup> Sun Yat-Sen University. &nbsp;&nbsp;
            <sup>2</sup> The Hong Kong University of Science and Technology. &nbsp;&nbsp;
            <br>
            <sup>3</sup> Northwestern Polytechnical University. &nbsp;&nbsp;
            <sup>4</sup> North China Electric Power University. &nbsp;&nbsp;
            <br>
            <sup>5</sup> The Hong Kong University of Science and Technology (Guangzhou). &nbsp;&nbsp;
            <br>
        </h45>
        <sup>*</sup>Equal Contribution &nbsp;&nbsp;
        <sup>†</sup>Corresponding Authors
    </p>
    <a href="https://ieeexplore.ieee.org/abstract/document/10801474"><img alt="Paper" src="https://img.shields.io/badge/Paper-IEEE-blue"/></a>
    <a href="https://arxiv.org/abs/2409.02738"><img alt="Paper" src="https://img.shields.io/badge/Paper-arXiv-red"/></a>
    <a href='https://robotics-star.com/SOAR'><img src='https://img.shields.io/badge/Project_Page-SOAR-green' alt='Project Page'></a>
    <a href="https://www.bilibili.com/video/BV1G1421Q79m"><img alt="Bilibili" src="https://img.shields.io/badge/Video-Bilibili-purple"/></a>
    <a href="https://www.bilibili.com/video/BV1wEyHYjEAq"><img alt="Bilibili" src="https://img.shields.io/badge/Talk-Bilibili-pink"/></a>
</div>


## 📢 News

- **[09/10/2024]**: The code of SOAR is released. 
- **[30/06/2024]**: SOAR is accepted to IROS 2024 and selected as **oral presentation** (acceptance rate: 10%). 

## 📜 Introduction

**[IROS'24]** This repository maintains the implementation of "SOAR: Simultaneous Exploration and Photographing with Heterogeneous UAVs for Fast Autonomous Reconstruction".

The key modules of SOAR are detailed in this overview.
<p align="center">
  <img src="assets/videos/overview.gif" width = 90% height = 90%/>
</p>

And we also provide a special demo for IROS2024.
<p align="center">
  <img src="assets/videos/iros_demo.gif" width = 90% height = 90%/>
</p>

If you find this work useful in your research, please consider citing:

```bibtex
@inproceedings{zhang2024soar,
  title={SOAR: Simultaneous Exploration and Photographing with Heterogeneous UAVs for Fast Autonomous Reconstruction},
  author={Zhang, Mingjie and Feng, Chen and Li, Zengzhi and Zheng, Guiyong and Luo, Yiming and Wang, Zhu and Zhou, Jinni and Shen, Shaojie and Zhou, Boyu},
  booktitle={2024 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  pages={10975--10982},
  year={2024},
  organization={IEEE}
}
```
Please kindly star ⭐️ this project if it helps you. We take great efforts to develop and maintain it 😁.

## 🛠️ Installation

### Prerequisite

* ROS Noetic (Ubuntu 20.04) or ROS Melodic (Ubuntu 18.04)
* PCL
* Eigen

__For Marsim__:
```shell
sudo apt update
sudo apt install libglfw3-dev libglew-dev
```

__For GCOPTER__:
```shell
sudo apt update
sudo apt install libompl-dev
```

### Compilation

__Project__:

```shell
git clone https://github.com/Robotics-STAR-Lab/SOAR.git
cd SOAR
catkin_make
```
If you have installed ***Anaconda***, please use ```catkin_make  -DPYTHON_EXECUTABLE=/usr/bin/python3```.

__LKH-3.0.6__:
```shell
cd src/planner/utils/lkh_mtsp_solver/LKH
make -j
```

## 🚀 Quick Start

### __Pisa Cathedral__
```shell
source devel/setup.bash && roslaunch heterogeneous_manager rviz.launch
source devel/setup.bash && roslaunch heterogeneous_manager pisa.launch
```

<p align="center">
  <img src="assets/videos/pisa.gif" width = 60% height = 60%/>
</p>

### __Sydney Opera House__
```shell
source devel/setup.bash && roslaunch heterogeneous_manager rviz.launch
source devel/setup.bash && roslaunch heterogeneous_manager sydney.launch
```

<p align="center">
  <img src="assets/videos/sydney.gif" width = 60% height = 60%/>
</p>

### __NOTE__ 
Trigger the quadrotors to start planning with the `2D Nav Goal` when the terminal displays `wait for trigger`. All scenes are provided in `src/heterogeneous_manager/launch/XXX.launch`

If you want to use the GPU version of MARSIM, you can change the parameter "use_gpu" to `true` in `src/heterogeneous_manager/launch/XXX.launch`

```xml
<arg name="use_gpu" value="true" />
```

### **Adjusting the Number of Photographers**

> The current version temporarily only supports a single explorer.

You can modify the `pisa.launch` or `sydney.launch` file as follows:

```xml
  <!-- _NUM_ is the total number of explorer and photographers -->
  <arg name="drone_num" value="_NUM_" />

  ... ...

  <!-- Explorer -->
  <group ns="quad_0">
    <include file="$(find heterogeneous_manager)/launch/single_lidar_uav_exploration.xml">
      <arg name="drone_id" value="0" />

      ... ...
      
    </include>

    <group if="$(arg use_sim)">
      <include file="$(find heterogeneous_manager)/launch/single_lidar_uav.xml">
        <arg name="drone_id" value="0" />
        
        ... ...
        
        <!-- Adjust to the appropriate initial position. -->
        <arg name="init_x_" value="" />
        <arg name="init_y_" value="" />
        <arg name="init_z_" value="" />
        <arg name="init_yaw" value="" />

        ... ...

      </include>
    </group>
  </group>

  <!-- Photographer1 -->
  <group ns="quad_1">
    <include file="$(find heterogeneous_manager)/launch/single_camera_uav_exploration.xml">
      <arg name="drone_id" value="1" />
      
      ... ...

    </include>

    <group if="$(arg use_sim)">
      <include file="$(find heterogeneous_manager)/launch/single_camera_uav.xml">
        <arg name="drone_id" value="1"/>
        <!-- Adjust to the appropriate initial position. -->
        <arg name="init_x_" value=""/>
        <arg name="init_y_" value=""/>
        <arg name="init_z_" value=""/>
        <arg name="init_yaw" value=""/>
        <arg name="odom_topic" value="$(arg odom_topic)"/>
      </include>
    </group>
  </group>

  <!-- Other photographers' groups -->
  ... ...

  <!-- PhotographerX (X = _NUM_-1) -->
  <group ns="quad_X">
    <include file="$(find heterogeneous_manager)/launch/single_camera_uav_exploration.xml">
      <!-- Adjust to the appropriate drone_id = _NUM_-1 -->
      <arg name="drone_id" value="X" />
      
      ... ...

    </include>

    <group if="$(arg use_sim)">
      <include file="$(find heterogeneous_manager)/launch/single_camera_uav.xml">
        <!-- Adjust to the appropriate drone_id = _NUM_-1 -->
        <arg name="drone_id" value="X"/>
        <!-- Adjust to the appropriate initial position. -->
        <arg name="init_x_" value=""/>
        <arg name="init_y_" value=""/>
        <arg name="init_z_" value=""/>
        <arg name="init_yaw" value=""/>
        <arg name="odom_topic" value="$(arg odom_topic)"/>
      </include>
    </group>
  </group>
```

## 🤓 Acknowledgments

- [FC-Planner](https://github.com/HKUST-Aerial-Robotics/FC-Planner): An Efficient Global Planner for Aerial Coverage.
- [FUEL](https://github.com/HKUST-Aerial-Robotics/FUEL): An Efficient Framework for Fast UAV Exploration.
- [RACER](https://github.com/SYSU-STAR/RACER): A Rapid Exploration Framework for Multiple UAVs.
- [GCOPTER](https://github.com/ZJU-FAST-Lab/GCOPTER): A General-Purpose Trajectory Optimizer for Multicopters.
- [MARSIM](https://github.com/hku-mars/MARSIM): A Light-weight Point-realistic Simulator for LiDAR-based UAVs.

## 🤗 FC-family Works

#### 1. What is FC-family?

We aim to develop intelligent perception-centric flight to realize ***F***ast ***C***overage / re***C***onstruction / inspe***C***tion etc.

#### 2. Projects list

* [PredRecon](https://github.com/HKUST-Aerial-Robotics/PredRecon) (ICRA2023): Prediction-boosted Planner for Aerial Reconstruction.
* [FC-Planner](https://github.com/HKUST-Aerial-Robotics/FC-Planner) (ICRA2024): Highly Efficient Global Planner for Aerial Coverage.
* [SOAR](https://github.com/SYSU-STAR/SOAR) (IROS2024): Heterogenous Multi-UAV Planner for Aerial Reconstruction.
  
