# Calibration
## Step 1 : Download and catkin code_utils 、 imu_utils
```
cd ~/catkin_ws/src/
git clone https://github.com/gaowenliang/code_utils.git
git clone https://github.com/gaowenliang/imu_utils.git
cd ..
catkin build code_utils
catkin build imu_utils
```
## Step 2 : Download Kalibr tool
### Install library
```
sudo apt-get install python-setuptools python-rosinstall ipython libeigen3-dev libboost-all-dev doxygen libopencv-dev ros-melodic-vision-opencv ros-melodic-image-transport-plugins ros-melodic-cmake-modules software-properties-common software-properties-common libpoco-dev python-matplotlib python-scipy python-git python-pip ipython libtbb-dev libblas-dev liblapack-dev python-catkin-tools libv4l-dev
sudo apt update
sudo apt install python-igraph
```
### Install Kalibt
cd ~/catkin_ws/src/
git clone https://github.com/ethz-asl/kalibr.git
catkin build -DCMAKE_BUILD_TYPE=Release -j4

## Step 3 : Record bag file
```
rosbag record -O [bag_name] [topic_name1] [topic_name2]
```

## Step 4 :  Check bag file
```
rosbag info [bag_name]
```

## Step 5 : Cmaera calibrate
```
rosrun kalibr kalibr_calibrate_cameras --bag [bag_name] --topics [topic_name] --models pinhole-radtan pinhole-radtan --target april_6x6_80x80cm.yaml
```

## Step 6 : Verify cmaera information
```
rosrun kalibr kalibr_camera_validator --cam [yaml_name] --target april_6x6_80x80cm.yaml
```

## Step 7 : IMU calibrate
Place the sensor horizontally and let it remain stationary for 2 to 3 hours to collect IMU data.
```
rosbag record -O [bag_name] [topic_name1]
roslaunch imu_utils [sensor].launch
```
## Step 8 : Camera-IMU calibration
```
rosrun kalibr kalibr_calibrate_imu_camera --bag [bag_name] --cam [yaml_name] --imu [imu_yaml] --target april_6x6_80x80cm.yaml
```

