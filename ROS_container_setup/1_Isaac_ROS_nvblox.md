# Issac ROS Enviroment Setup (For PC)
## 1. Nvidia-container-runtime
### a. Install the repo for the distribution 
```ruby
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```

For pre-releases, we need to enable the experimental repos of all dependencies
```ruby
sudo sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```

For later disable the experimental repos of all dependencies, run:
```ruby
sudo sed -i -e '/experimental/ s/^/#/g' /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```

Update the nvidia-container-runtime repo key
```ruby
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
  ```

### b. Install the nvidia-container-runtime package
```ruby
sudo apt-get install nvidia-container-runtime
```

### c. Docker engine setup
Regsiter the nvidia runtime with daemon configuration file
```ruby
sudo tee /etc/docker/daemon.json <<EOF
{
    "runtimes": {
        "nvidia": {
            "path": "/usr/bin/nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}
EOF
sudo pkill -SIGHUP dockerd
```

## 2. Isaac ROS Development Enviroment Setup
Make sure step 1 is completed.

### a. Configure nvidia-container-runtime as the default runtime to docker
```ruby
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    },
    "default-runtime": "nvidia"
}
```

### b. Restart Docker
```ruby
sudo systemctl daemon-reload && sudo systemctl restart docker
```
Install Git LFS to pull down all large files
```ruby
sudo apt-get install git-lfs
```
```ruby
git lfs install --skip-repo
```
Create a ROS 2 workspace for Isaac ROS
```ruby
mkdir -p  ~/workspaces/isaac_ros-dev/src
echo "export ISAAC_ROS_WS=${HOME}/workspaces/isaac_ros-dev/" >> ~/.bashrc
source ~/.bashrc
```
## 3. Isaac ROS nvblox
```ruby
cd ~/workspaces/isaac_ros-dev/src
```
```ruby
git clone https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_common
```
```ruby
git clone --recurse-submodules https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_nvblox && \
    cd isaac_ros_nvblox && git lfs pull
```
https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_nvblox#try-more-examples
```
Launch the Docker container
```ruby
cd ~/workspaces/isaac_ros-dev/src/isaac_ros_common && \
  ./scripts/run_dev.sh
```
Install package-specified dependencies in the container, via rosdep
```ruby
cd /workspaces/isaac_ros-dev/ && \
    rosdep install -i -r --from-paths src --rosdistro humble -y --skip-keys "libopencv-dev libopencv-contrib-dev libopencv-imgproc-dev python-opencv python3-opencv nvblox"
```
Build and source the workspace
```ruby
cd /workspaces/isaac_ros-dev && \
  colcon build --symlink-install && \
  source install/setup.bash
```
Run this test to verify the installation is correct
```ruby
colcon test --executor sequential
```
Installation finished

# Launch Nvblox with nav2
In the terminal that inside the Docker container:
```ruby
source /workspaces/isaac_ros-dev/install/setup.bash && \
    ros2 launch nvblox_examples_bringup isaac_sim_example.launch.py
```
Open another Docker container in the second terminal
```ruby
cd ~/workspaces/isaac_ros-dev/src/isaac_ros_common && \
  ./scripts/run_dev.sh
```

*** If you cannot launch Docker in the second terminal because of the permission issue, try:
```ruby
sudo usermod -aG docker $USER
// And reboot the PC.
```
Try to run the example in the second terminal
```ruby
ros2 bag play src/isaac_ros_nvblox/nvblox_ros/test/test_cases/rosbags/nvblox_pol
```
## More examples here:
https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_nvblox#try-more-examples






