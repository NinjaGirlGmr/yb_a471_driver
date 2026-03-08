# yb_a471_driver

This package provides a ROS 2 Python node named `imu_node` and exposes it as a console entrypoint for a Yahboom a471 10-axis IMU:

- `ros2 run yb_a471_driver imu_node`

The node publishes:

- `/imu/data_raw` (`sensor_msgs/Imu`)
- `/imu/orientation` (`sensor_msgs/Imu`)

The driver subscribes to common IMU source topics (`/camera/imu`, `/imu/data`, etc.), forwards the latest IMU sample to `/imu/data_raw`, and publishes a reduced orientation-only message on `/imu/orientation`.

## Launch/Runtime Use

Expected from the Bluebot bringup scripts:

- `ros2 run yb_a471_driver imu_node`

Optional parameters:

- `source_topics` (string array): IMU topics to subscribe to
- `publish_rate` (double): output rate in Hz (default `50.0`)
- `raw_topic` (string): raw IMU topic (default `/imu/data_raw`)
- `orientation_topic` (string): orientation topic (default `/imu/orientation`)
- `frame_id` (string): frame for fallback messages (default `imu_link`)
- `fallback_publish` (bool): publish zeroed IMU fallback data if no source appears (default `true`)

## Build

From workspace root:

```bash
colcon build --packages-select yb_a471_driver
```

Then source:

```bash
source /opt/ros/humble/setup.bash
source /ssd/ros2_ws/install/setup.bash
```

## Package contents

- `package.xml`
- `setup.py`
- `resource/yb_a471_driver`
- `yb_a471_driver/imu_node.py`

The package is tracked in bluebot as a submodule:

`git@github.com:NinjaGirlGmr/yb_a471_driver.git`
