# A brief introduction and use of rviz2

rviz is a three-dimensional visualization platform in ROS. On the one hand, it can realize the graphical display of external information. On the other hand, it can also release control information to objects through rviz, thereby realizing the monitoring and control of robots.

## 1 Introduction to rviz2

The successful installation of ros2 indicates that rviz2 is also successfully installed, because the installation of ros2 includes rviz2.

Open a new terminal (shortcut <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd>) and enter the command to open rviz2

```bash
rviz2
```

Open rviz2 and the following interface will be displayed:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz-1.png
width ="500" align = "center">

## 2 Introduction to each area

+ On the left is the display list. The display is something that draws something in the 3D world and may have some options available in the display list.

+ Above is the toolbar, which allows the user to select multiple functions with various function keys

+ The middle part is the 3D view: it is the main screen for viewing various data in three dimensions. The background color, fixed frame, grid, etc. of the 3D view can be set in detail in the Global Options and Grid items displayed on the left.
+ Below is the time display area, including system time and ROS time.
+ On the right is the observation angle setting area, where different observation angles can be set.

In this section, we only give a rough introduction. If you want to know more details, you can go to the [User Guide](http://wiki.ros.org/rviz/UserGuide) to check it out.

## 3 mycobot_ros2 installation and update

- **M5 version: ** Please check the end of the [12.2.1 ROS2 installation](../12.2.1-ROS2 installation.md) section.

- **PI version (Ubuntu 20.04): **

`mycobot_ros2` is a ROS package launched by ElephantRobotics that is compatible with various types of desktop robotic arms.

Project address: https://github.com/elephantrobotics/mycobot_ros2

The official default workspace is `colcon_ws`.

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-10.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-11.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-12.png
width ="500" align = "center">

Then enter the following command:

```bash
cd ~/colcon_ws/src # Enter the src folder in the workspace
# Clone the code on github
git clone https://github.com/elephantrobotics/mycobot_ros2.git
cd .. # Return to the workspace
colcon build --symlink-install # Build the code in the workspace, --symlink-install: Avoid recompiling every time you adjust the python script
source install/setup.bash # Add environment variables
```

**Note:** If `/home/er/colcon_ws/src (equivalent to ~/colcon_ws/src)` directory, you need to delete the original `mycobot_ros2` first, and then execute the above command.

## 4 Simple use

**Start through the launch.py ​​file**

This example is based on the fact that you have completed [Environment Setup](../12.2.1-ROS2 Installation.md) and successfully copied the company's code from GitHub.

Open a console terminal (shortcut key <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd>)
Enter the following command to **ROS2 environment configuration**.

```
cd ~/colcon_ws
colcon build --symlink-install
source install/setup.bash
```

Enter again:

- mycobot 280-M5 version:

```bash
ros2 launch mycobot_280 test.launch.py
```

![image-20220519154315585](../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/ros2_open1.png)

Open rviz2 and get the following result:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/open-2.png
width ="500" align = "center">

If you want to learn more about rviz, you can go to the [official document](http://wiki.ros.org/rviz2) to view it

## 5 M5 version prerequisites

- Open the console terminal (shortcut key <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd>), open the terminal window to view the device name:

```bash
# View the device name of the robot arm
ls /dev/ttyUSB* # Old version myCobot280 M5

# If the terminal does not display the /dev/ttyUSB related name, you need to use the following command
ls /dev/ttyACM* # New version myCobot280 M5
```

- Grant serial port permissions to the robot:

```bash
# The default device name is /dev/ttyUSB0. If the device name is not the default value, you need to modify it.
sudo chmod 777 /dev/ttyUSB0 # Old version myCobot280 M5

sudo chmod 777 /dev/ttyACM0 # New version myCobot280 M5
```

Then enter the user password (**Note:** The password is not displayed, just enter it correctly).

# 280 series rviz user guide

## Robot arm control

### 1 Slider control

Open a command line and run:

- mycobot 280-M5 version:

```bash
# The default serial port name of mycobot 280-M5 version is "/dev/ttyUSB0" and the baud rate is 115200. The serial port name of some models is "dev/ttyACM0". If the default serial port name is wrong, you can change the serial port name to "/dev/ttyACM0".
ros2 launch mycobot_280 slider_control.launch.py
```

- mycobot 280-PI version:

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-10.jpg width ="500" align = "center"> <img src =../.../../../../../../resources/3-FunctionsAndApplications/6. developmentGuide/ROS/ROS2/rviz2/12.2.7-11.jpg width ="500" align = "center"> <img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-12.png width = "500" align = "center">

Then run the command:

```bash
# The default serial port name of mycobot 280-PI version is "/dev/ttyAMA0" and the baud rate is 1000000.
ros2 launch mycobot_280pi slider_control.launch.py
```

- mycobot 280-JetsonNano version:

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-10.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-11.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/12.2.7-12.png
width ="500" align = "center">

Then run the command:

```bash
# mycobot 280-JetsonNano version default serial port name is "/dev/ttyTHS1", baud rate is 1000000.
ros2 launch mycobot_280jn slider_control.launch.py
```

It will **open rviz and a slider component**, and you will see the following screen (the screen of the Raspberry Pi version is slightly different, which does not affect the use):

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280/caf-1.png
width ="500" align = "center">

Then you can **control the movement of the model in rviz by dragging the slider**. The real mycobot will move with it.

**Please note: Since the robot arm will move to the current position of the model when the command is entered, please make sure that the model in rviz does not appear to be through the model before you use the command**
**Do not drag the slider quickly after connecting the robot arm to prevent damage to the robot arm**

### 2 Model following

In addition to the above control, we can also **let the model follow the movement of the real robot arm**. Open a command line and run:

- mycobot 280-M5 version:
##### 2 Slider control

> **Note: This function only supports the control of the robot**

Open a command line and run:

- mycobot 280-M5 version:

```bash
# The default serial port name of mycobot 280-M5 version is "/dev/ttyUSB0" and the baud rate is 115200. The serial port name of some models is "dev/ttyACM0". If the default serial port name is wrong, the serial port name can be changed to "/dev/ttyACM0".
ros2 launch mycobot_280 slider_control_pump.launch.py
```

- mycobot 280-PI version:

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-10.jpg width ="500" align = "center"> 

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280/12.2.7-11.jpg width ="500" align = "center"> 

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-12.png
width ="500" align = "center">

Then run the command:

```bash
# The default serial port name of mycobot 280-PI version is "/dev/ttyAMA0" and the baud rate is 1000000.
ros2 launch mycobot_280pi slider_control_pump.launch.py
```

It will **open rviz and a slider component**, and you will see the following screen (the screen of the Raspberry Pi version is slightly different, which does not affect the use):

<img src =../../../resourse/12-ApplicationBaseROS/12.1.4-16.png
width ="500" align = "center">

Then you can **control the model movement in rviz by dragging the slider**. The real mycobot will move with it.

**Please note: Since the robot arm will move to the current position of the model when the command is input, please make sure that the model in rviz does not appear to be through the model before you use the command**

**Do not drag the slider quickly after connecting the robot arm to prevent damage to the robot arm**

##### 3 GUI control

Based on the previous, this package also **provides a simple Gui control interface**. This method is intended for real robots to interact with each other. Please connect mycobot.

Open the command line:

- mycobot 280-M5 version:

```bash
# The default serial port name of mycobot 280-M5 version is "/dev/ttyUSB0" and the baud rate is 115200. The serial port name of some models is "dev/ttyACM0". If the default serial port name is wrong, you can change the serial port name to "/dev/ttyACM0".
ros2 launch mycobot_280 simple_gui_pump.launch.py
```

It will **open rviz and a GUI interface**, and you will see the following screen:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.1.4-14.png
width ="500" align = "center">

#### 5.2 Camera flange

##### 1 Load the model

Open a command line and run:

- mycobot 280-M5 version:

```bash
ros2 launch mycobot_280 test_camera_flange.launch.py
```

- mycobot 280-PI version:

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-10.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-11.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-12.png
width ="500" align = "center">

Then run the command:

```bash
ros2 launch mycobot_280pi test_camera_flange.launch.py
```

It will **open rviz**, you will see the following screen (the screen of the Raspberry Pi version is slightly different, which does not affect the use):

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.1.4-15.png
width ="500" align = "center">

##### 2 Slider control

> **Note: This function only supports the control of the robot arm**

Open a command line and run:

- mycobot 280-M5 version:

```bash
# The default serial port name of the mycobot 280-M5 version is "/dev/ttyUSB0" and the baud rate is 115200. The serial port name of some models is "dev/ttyACM0", if the default serial port name is wrong, you can change the serial port name to "/dev/ttyACM0".
ros2 launch mycobot_280 slider_control_camera_flange.launch.py
```

- mycobot 280-PI version:

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-10.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-11.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-12.png
width ="500" align = "center">

Then run the command:

```bash
# The default serial port name of mycobot 280-PI version is "/dev/ttyAMA0" and the baud rate is 1000000.
ros2 launch mycobot_280pi slider_control_camera_flange.launch.py
```

It will **open rviz and a slider component**, and you will see the following screen (the screen of the Raspberry Pi version is slightly different, which does not affect the use):

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.1.4-17.png
width ="500" align = "center">

Then you can **control the movement of the model in rviz by dragging the slider**. The real mycobot will move with it.

**Please note: Since the robot arm will move to the current position of the model when the command is entered, please make sure that the model in rviz does not appear to be through the model before you use the command**.
**Do not drag the slider quickly after connecting the robot arm to prevent damage to the robot arm**.

#### 5.3 Camera flange && pump

##### 1 Load the model

Open a command line and run:

- mycobot 280-M5 version:

```bash
ros2 launch mycobot_280 test_camera_flange_pump.launch.py
```

- mycobot 280-PI version:

Click the `ROS2 Shell` icon on the desktop or the corresponding icon in the bar below the desktop to open the ROS2 environment terminal:

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-10.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-11.jpg
width ="500" align = "center">

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.2.7-12.png
width ="500" align = "center">

Then run the command:

```bash
ros2 launch mycobot_280pi test_camera_flange_pump.launch.py
```

It will **open rviz**, you will see the following screen (the screen of the Raspberry Pi version is slightly different, which does not affect the use):

<img src =../.../../../../../../resources/3-FunctionsAndApplications/6.developmentGuide/ROS/ROS2/rviz2/rviz2-280//12.1.4-18.png
width ="500" align = "center">

#### 5.3 URDF model address

##### 1 myCobot vertical suction pump V2.0

- [myCobot 280-M5 version](https://github.com/elephantrobotics/mycobot_ros2/blob/280-ros-pump-camera/mycobot_description/urdf/mycobot/mycobot_with_pump.urdf)

- [myCobot 280-PI version](https://github.com/elephantrobotics/mycobot_ros2/blob/280-ros-pump-camera/mycobot_description/urdf/mycobot_pi/mycobot_with_pump.urdf)

##### 2 Camera flange

- [myCobot 280-M5 Version](https://github.com/elephantrobotics/mycobot_ros2/tree/humble/mycobot_description/urdf/mycobot/mycobot_with_camera_flange.urdf)

- [myCobot 280-PI Version](https://github.com/elephantrobotics/mycobot_ros2/tree/humble/mycobot_description/urdf/mycobot_pi/mycobot_with_camera_flange.urdf)

##### 3 Camera Flange && Pump

- [myCobot 280-M5 Version](https://github.com/elephantrobotics/mycobot_ros2/tree/humble/mycobot_description/urdf/mycobot/mycobot_with_camera_flange_pump.urdf)

- [myCobot 280-PI version](https://github.com/elephantrobotics/mycobot_ros2/tree/humble/mycobot_description/urdf/mycobot_pi/mycobot_with_camera_flange_pump.urdf)