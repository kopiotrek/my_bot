ARG ROS_DISTRO=humble
FROM osrf/ros:$ROS_DISTRO-desktop

ARG DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-c"]
RUN apt update && \
    apt-get install -y ros-$ROS_DISTRO-xacro ros-$ROS_DISTRO-ros2-control ros-$ROS_DISTRO-ros2-controllers \
    ros-$ROS_DISTRO-gazebo-ros-pkgs ros-$ROS_DISTRO-gazebo-ros2-control ros-$ROS_DISTRO-robot-localization \
    ros-$ROS_DISTRO-slam-toolbox ros-$ROS_DISTRO-rmw-cyclonedds-cpp wget make \
    && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc
COPY ros_entrypoint.sh /
ENTRYPOINT ["../ros_entrypoint.sh"]
RUN chmod +x /ros_entrypoint.sh

WORKDIR /app
COPY src src

RUN cd /app && source /opt/ros/$ROS_DISTRO/setup.bash && colcon build