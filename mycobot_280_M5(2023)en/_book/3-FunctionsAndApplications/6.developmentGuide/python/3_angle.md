# Joint Control

For serial multi-joint robots, the control of joint space is to control the variables of each joint of the robot, and the goal is to make each joint of the robot reach the target position at a certain speed.

> **Note:** When setting the angle, the limit of different series of robot arms is different. For details, please refer to the parameter introduction of the corresponding model.

## myCobot

### Single joint control

**send_angle(id, degree, speed)**

- **Function:** Send the specified single joint movement to the specified angle

- **Parameter description:**

- `id`: Represents the joint of the robot arm. The six-axis has six joints and the four-axis has four joints. There is a specific representation method

Joint 1 representation: `Angle.J1.value` (can also be represented by numbers 1-6)

- `degree`: Represents the angle of the joint

- `speed`: Represents the speed of the robot arm movement, ranging from 0 to 100

- **Return value:** None

**set_encoder(joint_id, encoder)**

- **Function:** Send the specified single joint movement to the specified potential value

- **Parameter description:**

- `joint_id`: Represents the joint of the robot arm. The six-axis has six joints and the four-axis has four joints. There is a specific representation method
The representation of joint 1: `Angle.J1.value` (can also be represented by numbers 1-6)
- `encoder`: represents the potential value of the robot arm, the value range is 0 ~ 4096
- **Return value: ** None

### Multi-joint control

**get_angles()**

- **Function: ** Get all joint angles

- **Return value: ** `list` A list of floating point values, representing the angles of all joints

**send_angles(degrees, speed)**

- **Function: ** Send all angles to all joints of the robot arm
- **Parameter description: **
- `degrees`: `(List[float])` contains the angles of all joints. The six-axis robot has six joints, so the length is 6, and the four-axis length is 4. For example, the representation of the six-axis is: `[20,20,20,20,20,20]`
- `speed`: Indicates the speed of the robot arm, the value range is 0-100
- **Return value:** None

**set_encoders(encoders, sp)**

- **Function:** Send potential values ​​to all joints of the robot arm
- **Parameter description:**
- `encoder`: Indicates the potential value of the robot arm, the value range is 0 ~ 4096, the length of the six-axis is 6, the length of the four-axis is 4, such as the representation method of the six-axis: `[2048,2048,2048,2048,2048,2048]`
- `sp`: Indicates the speed of the robot arm, the value range is 0-100
- **Return value:** None

**sync_send_angles(degrees, speed, timeout=7)**

- **Function:** Synchronously send angles and return when reaching the target point
- **Parameter description:**
- `degrees`: List of angle values ​​of each joint `List[float]`
- `speed`: (`int`) The speed of the robot arm, the value range is 0-100
- `timeout`: The default time is 7s

**get_radians()**

- **Function:** Get the radians of all joints
- **Return value:** `list` contains a list of all joint radian values

**send_radians(radians, speed)**

- **Function:** Send radian values ​​to all joints of the robot arm
- **Parameter description:**
- `radians`: Indicates the radian value of the robot arm, the value range is -5~5
- **Return value:** `list` contains a list of all joint radian values

### Example use

```python
from pymycobot.mycobot import MyCobot
from pymycobot.genre import Angle
from pymycobot import PI_PORT, PI_BAUD # When using the Raspberry Pi version of mycobot, you can reference these two variables to initialize MyCobot
import time

# MyCobot Class initialization requires two parameters:
# The first is the serial port string, such as:
# linux: "/dev/ttyUSB0"
# windows: "COM3"
# The second is the baud rate:
# M5 version: 115200
#
# For example:
# mycobot-M5:
# linux:
# mc = MyCobot("/dev/ttyUSB0", 115200)
# windows:
# mc = MyCobot("COM3", 115200)
# mycobot-raspi:
# mc = MyCobot(PI_PORT, PI_BAUD)
#
# Initialize a MyCobot object
# Here is the object code for the windows version
mc = MyCobot("COM3", 115200)
# By passing the angle parameter, each joint of the robot arm moves to the corresponding position [0, 0, 0, 0, 0, 0]
mc.send_angles([0, 0, 0, 0, 0, 0], 50)

# Set the waiting time to ensure that the robot has reached the specified position
time.sleep(2.5)

# Move joint 1 to the position of 90
mc.send_angle(Angle.J1.value, 90, 50)

# Set the waiting time to ensure that the robot has reached the specified position
time.sleep(2)

# The following code can make the robot swing left and right
# Set the number of loops
num=5
while num > 0:
# Move joint 2 to the position of 50
mc.send_angle(Angle.J2.value, 50, 50)

# Set the waiting time to ensure that the robot has reached the specified position
time.sleep(1.5)

# Move joint 2 to the position of -50
mc.send_angle(Angle.J2.value, -50, 50)

# Set the waiting time to ensure that the robot has reached the specified position
time.sleep(1.5)

num -= 1

# Retract the robot arm. You can swing the robot arm manually, and then use the get_angles() function to get the coordinate sequence.
# Use this function to make the robot arm reach the position you want.
mc.send_angles([88.68, -138.51, 155.65, -128.05, -9.93, -15.29], 50)

# Set the waiting time to ensure that the robot arm has reached the specified position
time.sleep(2.5)

# Relax the robot arm and swing it manually
mc.release_all_servos()
```