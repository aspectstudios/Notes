

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
