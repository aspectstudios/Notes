

Instructions for https://github.com/leggedrobotics/darknet_ros:
---

0.	Create a catkin workspace:

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/

```

1.	Download the leggedrobotics repo, `git clone --recursive https://github.com/leggedrobotics/darknet_ros.git`


2. Edit the CUDA compute compatibility, in `~/catkin_ws/darknet_ros/darknet_ros/CMakeLists.txt`:
```
${CUDA_NVCC_FLAGS};
-O3
-gencode arch=compute_52,code=[sm_52,compute_52]

```

4. Copy the weights files into `catkin_ws/src/darknet_ros/darknet_ros/yolo_network_config/weights/`

5. Ensure there are matching config files in `/home/edanweis/catkin_ws/src/darknet_ros/darknet_ros/yolo_network_config/cfg/`

6. Run `catkin build darknet_ros -DCMAKE_BUILD_TYPE=Release`

7. Go to `catkin_ws` and run a test with `catkin build darknet_ros --no-deps --verbose --catkin-make-args run_tests`

8. Customise `.conf` files with `use_darknet: true`, `threshold` and `wait_key_delay: 1`.

9. Clone usb_cam, from `https://github.com/ros-drivers/usb_cam.git` into `catkin_ws/src` make with `catkin make --pkg usb_cam` ? and then source `catkin_ws/devel/setup.bash`. 

10. Overlay the source after making usb_cam with `source ./devel/setup.bash`

11. Start usb_cam with `rosrun usb_cam usb_cam-test.launch` ?

12. Run `rosrun roslaunch darknet_ros darknet_ros.launch`



Notes on setting up Linux, CUDA, etc.
---

Install Nvidia drivers: [https://askubuntu.com/a/700613](https://askubuntu.com/a/700613)  

Install I-Nex to examine GPU  

Install CUD, Download Installers for Linux Ubuntu 16.04 x86_64:  
[https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)  

Add the following to ~/.bashrc  
[https://askubuntu.com/a/889332](https://askubuntu.com/a/889332)  

ROS Kinetic  
follow instructions on wiki. Set your ROS_WORKSPACE as ~/catkin_ws in ~/.bashrc  

You might need to set  
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH  

usb_camera issue:  
[https://github.com/ros-drivers/usb_cam/issues/43](https://github.com/ros-drivers/usb_cam/issues/43)  

[http://www.iheartrobotics.com/2010/05/testing-ros-usb-camera-drivers.html](http://www.iheartrobotics.com/2010/05/testing-ros-usb-camera-drivers.html)  

HD Pro Webcam C920 (usb-0000:08:00.0-1.1):  
/dev/video0  

[http://www.iheartrobotics.com/2010/05/testing-ros-usb-camera-drivers.html](http://www.iheartrobotics.com/2010/05/testing-ros-usb-camera-drivers.html)  

Try this if getting error: unknown type name ‘CvCapture’  
image get_image_from_stream(CvCapture *cap);  
[https://stackoverflow.com/questions/42523545/error-in-build-project-with-opencv](https://stackoverflow.com/questions/42523545/error-in-build-project-with-opencv)  

CUDA scores:  
[https://developer.nvidia.com/cuda-gpus](https://developer.nvidia.com/cuda-gpus)  

Boost:  
[https://stackoverflow.com/questions/12578499/how-to-install-boost-on-ubuntu](https://stackoverflow.com/questions/12578499/how-to-install-boost-on-ubuntu)  

Install catkin cmd tools  
[http://catkin-tools.readthedocs.io/en/latest/installing.html](http://catkin-tools.readthedocs.io/en/latest/installing.html)  

might have to install also:  
pip install catkin_pkg  
pip install empy  

OpenCV instructions:  
[http://www.pyimagesearch.com/2015/07/27/installing-opencv-3-0-for-both-python-2-7-and-python-3-on-your-raspberry-pi-2/](http://www.pyimagesearch.com/2015/07/27/installing-opencv-3-0-for-both-python-2-7-and-python-3-on-your-raspberry-pi-2/)  

OpenCV cmake command:  

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -DWITH_QT=ON -DWITH_LAPACK=OFF -DWITH_IPP=ON -DWITH_OPENGL=ON -DFORCE_VTK=ON -DWITH_TBB=ON -DWITH_GDAL=ON -DWITH_XINE=ON -DBUILD_EXAMPLES=ON -DOPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.2.0/modules -DBUILD_opencv_world=OFF -DCUDA_NVCC_FLAGS="-D_FORCE_INLINES" -DPYTHON_EXECUTABLE=~/.virtualenvs/cv3/bin/python -DENABLE_PRECOMPILED_HEADERS=OFF ..  

Darknet ROS  
[https://github.com/leggedrobotics/darknet_ros](https://github.com/leggedrobotics/darknet_ros)  

roslaunch darknet_ros object_detect.launch  

