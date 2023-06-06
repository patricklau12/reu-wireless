# Jun 6, 2023
## 1. Install SSD
i. Flip the Orin Nano
ii. Insert the SSD into the M.2 slot  
(SAMSUNG SSD 970 EVO Plus is used)

## 2. Flashing Jetson Linux 
### Method 1: Using SDK Manager
i. Connect Jetson Orin Nano with the host computer 
ii. Follow the instructions of SDK Manager
### Method 2: From command line
i. Connect Jetson Orin Nano with the host computer 
#### In the host computer,
```ruby
git clone https://github.com/jetsonhacks/bootFromExternalStorage.git
```

```ruby
cd bootFromExternalStorage
./get_jetson_files.sh
cd R35.3.1
cd Linux_for_Tegra/
```

#### In the Jetson Orin Nano
Prepare for flashing
i. Remove power
ii. Put the Nano into Force Recovery Mode (Short pin "FC REC" and "GND" with jumper wire)
iii. Connect Nano and host PC with USB-C & USB cable
iv. Go back to the host computer's terminal, /bootFromExternalStorage
v. ./flash_jetson_external_storage.sh (takes ~20mins)
====================================================================================================
## 3. Installing Jetpack
```ruby
apt-cache depends nvidia-jetpack
apt-cache depends nvidia-jetpack-runtime
apt-cache depends nvidia-jetpack-dev
apt-cache depends nvidia-vpi-dev
sudo apt update
sudo apt install nvidia-jetpack
```



