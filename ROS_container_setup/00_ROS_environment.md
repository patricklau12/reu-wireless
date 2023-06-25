# ROS Environment Setup
For Workstation
- Ubuntu 22.04

## Repository Configuration
https://nvidia.github.io/nvidia-container-runtime/
```
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```
```
sudo sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```
```
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
```
## Docker Installation
https://docs.docker.com/engine/install/ubuntu/
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt-get update
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verify by running hello-world
```
sudo docker run hello-world
```
## nvidia-docker 2 Installation
https://github.com/nvidia/nvidia-docker/wiki/Installation-(version-2.0)
```
sudo apt-get install nvidia-docker2
sudo pkill -SIGHUP dockerd
```

## nvidia-container-runtime Installation
https://github.com/NVIDIA/nvidia-container-runtime#installation
```
sudo apt-get install nvidia-container-runtime
```
Edit /etc/docker/daemon.json to below:
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
```
sudo systemctl daemon-reload && sudo systemctl restart docker
```
```
sudo apt-get install git-lfs
```
```
git lfs install --skip-repo
```
Create ROS2 workspace for experimenting with Isaac ROS
```
mkdir -p  ~/workspaces/isaac_ros-dev/src
echo "export ISAAC_ROS_WS=${HOME}/workspaces/isaac_ros-dev/" >> ~/.bashrc
source ~/.bashrc
```



