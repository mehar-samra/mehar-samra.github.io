## Running Infiniworkflow on Nvidia Jetson


The Jetson is a series of embedded computing boards primarily designed for applications in robotics / drones, cameras, and medical equipment. The Nvidia Jetson that we are using is the Nvidia Jetson Orin Nano Dev Kit, which is far from the strongest computer available but is still strong enough to run Infiniworkflow with CUDA enabled. 

The process of getting Infiniworkflow to run on the Jetson took a fair amount of time, as we had to get the Jetson up and running first and foremost before getting to anything else. 

The process of getting the Nvidia Jetson running from scratch is as follows:
1. The Jetson Nano may have old firmware installed. To check, plug the Jetson (without a memory card) into a monitor, connect the power source to the Jetson, and check the 3rd line that will appear on the screen to see if the firmware is less or greater than or equal to version 36.0. If the firmware is < 36.0, there will be several more steps, which can be found here: https://www.jetson-ai-lab.com/initial_setup_jon.html. You can disconnect power to the Jetson Nano at this point.

2. Download the latest JetPack 6.x image onto your regular computer. The link to the download can be found in the green box within Step 6.1 of the same website: https://www.jetson-ai-lab.com/initial_setup_jon.html

3. Connect your SD card to your computer, and use an external application such as Balena Etcher to flash the image to your SD card.

4. Insert the SD card with JetPack 6.x into the back slot of the Jetson Nano

5. Plug the power source into the Jetson, and complete the initial software setup / configuration.

6. With step 5 done, a firmware update should be automatically scheduled, so reboot the Jetson Nano to trigger the final firmware update.

To get more storage on the Jetson Nano, you can connect a NVMe SSD to the Jetson in addition to the microSD card. 


The code to get Infiniworkflow running on Jetson was similar enough to the Linux code, but there were still a number of adjustments that had to be made because of the Jetson's extremely simple design (unlike on Windows or Mac). The Jetson now has its own folder within the Infiniworkflow directory, which now includes its own installer along with a script that adds OpenCV to Nvidia Jetson. A snippet of the code can be seen below:

`
# install the common dependencies
  sudo apt-get install -y cmake
  sudo apt-get install -y libjpeg-dev libjpeg8-dev libjpeg-turbo8-dev
  sudo apt-get install -y libpng-dev libtiff-dev libglew-dev
  sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev
  sudo apt-get install -y libgtk2.0-dev libgtk-3-dev libcanberra-gtk*
  sudo apt-get install -y python3-pip
  ...
# remove old versions or previous builds
  cd ~ 
  sudo rm -rf opencv*
# download the latest version
  git clone --depth=1 https://github.com/opencv/opencv.git
  git clone --depth=1 https://github.com/opencv/opencv_contrib.git
# set install dir
  cd ~/opencv
  mkdir build
  cd build
# run cmake
  cmake -D CMAKE_BUILD_TYPE=RELEASE \
  -D BUILD_opencv_world=ON \
  -D CMAKE_INSTALL_PREFIX=/usr \
  -D CMAKE_INSTALL_PREFIX=/usr \
  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
  -D EIGEN_INCLUDE_PATH=/usr/include/eigen3 \
  -D WITH_OPENCL=OFF \
  -D CUDA_ARCH_BIN=${ARCH} \
  -D CUDA_ARCH_PTX=${PTX} \
  -D WITH_CUDA=ON \
  -D WITH_CUDNN=ON \
  ...
 ...
# cleaning (frees 320 MB)
  make clean
  sudo apt-get update
  echo "Congratulations!"
  echo "You've successfully installed OpenCV 4.11.0 on your Nano"
`

Adding access to Nvidia Jetson devices was important, as it means we can open up a new paradigm for integrating Infiniworkflow into daily usage by workers of any kind. Consider this example: a factory has Jetson machines, with Infiniworkflow running on the Jetson to monitor the assembly line, but workers from the company can log in from their home or office and connect to Infiniworkflow to create workflows, control the cameras, and create AI/ML inference workflows, all remotely. This is because Infiniworkflow would be running on the Jetson at all times, but the frontend could go to any PC, as long as it's connected to the local LAN or the internet.






