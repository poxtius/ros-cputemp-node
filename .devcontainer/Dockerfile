FROM osrf/ros:noetic-desktop-full

# Update all packages
RUN apt update && apt upgrade -y

# Install extra packages
RUN apt install gdb -y
RUN apt install git -y

# Rosdep update
RUN rosdep update

# Add ros user
ARG USERNAME=ros
RUN groupadd --gid 1000 $USERNAME && \
    useradd --uid 1000 --gid 1000 -ms /bin/bash $USERNAME && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

## Make sure to reflect new user in PATH
ENV PATH="/home/${USERNAME}/.local/bin:${PATH}"
USER $USERNAME

# Source the ROS noetic setup file
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc

WORKDIR /tmp
