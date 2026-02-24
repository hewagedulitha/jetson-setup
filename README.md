# jetson-setup

`conda activate rl`

`jetson-containers run -v /home/hewaged/ae-mnt:/ae --device=/dev/ttyTHS1  $(autotag l4t-pytorch)`

`cd /ae/aae-train-donkeycar/ && pip install -e . --index-url https://pypi.org/simple
pip install numpy==1.26.4 --index-url https://pypi.org/simple
`

`cd ..
pip install stable-baselines3 --index-url https://pypi.org/simple
pip3 install pyserial --index-url https://pypi.org/simple 
cd /ae/
env "PATH=$PATH" python3 nav.py
`

start realsense container

`conda activate rl`

`jetson-containers run -v volume:/volume  -v /home/hewaged/ae-mnt:/ae  $(autotag realsense_ros)`

`cd /volume/ros2_ws/ && . install/local_setup.bash`

run this line after starting the image saver docker

`cd /ae/ && ros2 run realsense2_camera realsense2_camera_node`

if ROS is not working across docker containers, open new terminal on the same container

`sudo docker ps # get container name for the realsense container instance`

`sudo docker exec -it jetson_container_20260216_101449 bash`

source ros installation

`source /opt/ros/humble/install/setup.bash`

source image node

`cd /ae/image_ws/
source install/setup.bash
pip3 install numpy==1.21.5
ros2 run py_srvcli2 subscriber`


`sudo docker run -it -v /home/hewaged/ae-mnt:/ae realsense_ros:latest-l4t-r36.4.4
cd ae
ros2 run image_view image_saver image:=/camera/camera/color/image_raw --ros-args -p  save_all_image:=false -p filename_format:="image.png"`


`sudo docker run -it -v /home/hewaged/ae-mnt/:/ae --network host realsense_ros:latest-l4t-r36.4.4
pip3 install numpy==1.21.5
cd ae/image_ws/
source install/setup.bash
ros2 run py_srvcli2 subscriber`

OR

`cd ae/ && ./save_image.sh`
