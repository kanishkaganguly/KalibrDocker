# Base image for ROS Indigo Desktop Full
FROM osrf/ros:indigo-desktop-full

# Install dependencies
RUN apt-get update && apt-get install -y \
    python-setuptools \
    python-rosinstall \
    ipython \
    libeigen3-dev \
    libboost-all-dev \
    doxygen \
    libopencv-dev \
    ros-indigo-vision-opencv \
    ros-indigo-image-transport-plugins \
    ros-indigo-cmake-modules \
    python-software-properties \
    software-properties-common \
    libpoco-dev \
    python-matplotlib \
    python-scipy \
    python-git \
    python-pip \
    ipython \
    libtbb-dev \
    libblas-dev \
    liblapack-dev \
    python-catkin-tools \
    libv4l-dev \
    wget
RUN pip install python-igraph --upgrade

# Catkin workspace and setup
RUN mkdir -p /root/workspace/src
WORKDIR /root/workspace
RUN ["/bin/bash", "-c", "source /opt/ros/indigo/setup.bash"]
RUN ["/bin/bash", "-c", "catkin init"]
RUN ["/bin/bash", "-c", "catkin config --extend /opt/ros/indigo"]
RUN ["/bin/bash", "-c", "catkin config --merge-devel"]
RUN ["/bin/bash", "-c", "catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release"]

# Clone and build Kalibr
RUN git clone https://github.com/ethz-asl/Kalibr.git /root/workspace/src/Kalibr
WORKDIR /root/workspace
RUN ["/bin/bash", "-c", "catkin build -DCMAKE_BUILD_TYPE=Release -j8"]
RUN ["/bin/bash", "-c", "source /root/workspace/devel/setup.bash"]
