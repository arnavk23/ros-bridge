# ROS Humble ↔ ROS Noetic Bridge (Ubuntu 24.04)

This repository provides a Docker-based setup to bridge **ROS 2 Humble** with **ROS 1 Noetic** on **Ubuntu 24.04**, enabling message and service communication across both ecosystems using `ros1_bridge`.

## Features

- Dockerfile-based reproducible setup
- Bridges topics and services between ROS Noetic (ROS 1) and ROS Humble (ROS 2)
- Supports running on Ubuntu 24.04
- Minimal dependencies and isolated environment

## Prerequisites

- Docker (v20.10+)
- Docker Compose (optional, for easier multi-container setup)
- Ubuntu 24.04 host (or compatible)

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/arnavk23/ros-bridge.git
cd ros-bridge
````

### 2. Build the Docker Image

```bash
docker build -t ros-bridge .
```

### 3. Run the Container

```bash
docker run -it --rm \
    --net=host \
    --env="DISPLAY" \
    ros-bridge
```

> The `--net=host` flag ensures ROS 1/2 networking works correctly across environments.

### 4. Using the Bridge

Inside the container:

```bash
source /opt/ros/humble/setup.bash
source /opt/ros/noetic/setup.bash
source /ros_ws/install/setup.bash

ros2 run ros1_bridge dynamic_bridge
```

This will automatically detect and bridge common messages/services between the two ROS versions.

## Customization

* Add additional ROS packages to `ros_ws/src/` and rebuild using `colcon build`.
* Modify the `Dockerfile` if you need GPU support, custom dependencies, or additional tools.

## Testing

1. Launch a ROS 1 publisher (e.g., `rostopic pub`)
2. Launch a ROS 2 subscriber (e.g., `ros2 topic echo`)
3. Verify messages flow between the systems via the bridge.

## Notes

* Ubuntu 24.04 support for ROS Noetic and Humble may involve workarounds, since Noetic is officially supported up to Ubuntu 20.04.
* For fully working bridges, message types must be **identical** in both ROS 1 and ROS 2.
---
