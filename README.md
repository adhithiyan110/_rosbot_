
## Installation

## URDF

```bash
sudo apt install ros-foxy-xacro ros-foxy-joint-state-publisher-gui
```

## ros_serial_demo
git clone in both devices
```bash
git clone https://github.com/joshnewans/serial_motor_demo.git
```
```bash
sudo apt install python3-serial
```

    

- [Arduino code link](https://github.com/joshnewans/ros_arduino_bridge.git)


#### pin configuration


| Arduino pin | L298N pin     |
| :-------- | :------- | 
| D10 | IN2 | 
| D6   | IN1 |
| D9  | IN3 |
| D5  | IN4 |


| Arduino pin | Encoder pin    |
| :-------- | :------- | 
| D2 | left A | 
| D3   | left B |
| A4  | right A|
| A5  | right B |

The main commands to know are

- `e` - Motor responds with current encoder counts for each motor
- `r` - Reset encoder values
- `o <PWM1> <PWM2>` - Set the raw PWM speed of each motor (-255 to 255)  (example o 255 255)
- `m <Spd1> <Spd2>` - Set the closed-loop speed of each motor in *counts per loop* (Default loop rate is 30, so `(counts per sec)/30` (example m 115 115)
- `p <Kp> <Kd> <Ki> <Ko>` - Update the PID parameters

#### START COMMAND
```bash
miniterm -e /dev/ttyUSB0 57600
```

#### command in orin
```bash
ros2 run serial_motor_demo driver --ros-args -p encoder_cpr:=3440 -p loop_rate:=30 -p serial_port:=/dev/ttyUSB0 -p baud_rate:=57600
```

#### command in host
```bash
ros2 run serial_motor_demo gui
```

## ros2_control
```bash
sudo apt install ros-foxy-ros2-control ros-foxy-ros2-controllers ros-foxy-gazebo-ros2-control
```

```bash
ros2 control list_hardware_interfaces
```
```bash
ros2 control list_controllers
```
```bash
ros2 run controller_manager spawner.py diff_cont
```
```bash
ros2 run controller_manager spawner.py joint_broad
```

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/diff_cont/cmd_vel_unstamped
```
