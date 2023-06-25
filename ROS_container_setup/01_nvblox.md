# ISAAC ROS Nvblox 
https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_nvblox#quickstart

Isaac ROS Nvblox contains ROS 2 packages for 3D reconstruction and cost maps for navigation.

## Steps
```
cd ~/workspaces/isaac_ros-dev/src
```
```
git clone https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_common
```
```
git clone --recurse-submodules https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_nvblox && \
    cd isaac_ros_nvblox && git lfs pull
```
```
cd ~/workspaces/isaac_ros-dev/src/isaac_ros_nvblox && git lfs pull -X "" -I "nvblox_ros/test/test_cases/rosbags/nvblox_pol"
```
```
cd ~/workspaces/isaac_ros-dev/src/isaac_ros_common && \
  ./scripts/run_dev.sh
```
```
cd /workspaces/isaac_ros-dev/ && \
    rosdep install -i -r --from-paths src --rosdistro humble -y --skip-keys "libopencv-dev libopencv-contrib-dev libopencv-imgproc-dev python-opencv python3-opencv nvblox"
```
```
cd /workspaces/isaac_ros-dev && \
  colcon build --symlink-install && \
  source install/setup.bash
```
```
colcon test --executor sequential
```