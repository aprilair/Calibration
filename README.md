# Calibration
## Step 1 : Download Kalibr tool
[Kalibr](https://github.com/ethz-asl/kalibr)

## Step 1 : Record bag file
```
rosbag record -O [bag_name] [topic_name1] [topic_name2]
```

## Step 2 :  Check bag file
```
rosbag info [bag_name]
```

## Step 3 : Cmaera calibrate
```
rosrun kalibr kalibr_calibrate_cameras --bag [bag_name] --topics [topic_name] --models pinhole-radtan pinhole-radtan --target april_6x6_80x80cm.yaml
```

## Step 4 : Verify cmaera information
```
rosrun kalibr kalibr_camera_validator --cam [yaml] --target april_6x6_80x80cm.yaml
```

## Step 5 : IMU calibrate
```

