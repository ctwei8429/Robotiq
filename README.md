# Robotiq Gripper
Robotiq 2F-85 Grippers Control in Robot Operating System

The 2-Finger Gripper comes with either 85 mm opening (2-Finger 85).

## 2-finger 85 Specification
   Device Name                           | 2-Finger 85
   --------------------------------------|:---------------------------------------:| 
   Input Voltage Range                   | 24 V (DC) ±10%
   Absolute maximum supply voltage 2     | 28 V DC
   Peak current                          | 1 A    
   Gripper Opening                       | 85 mm
   Minimum diameter for encompassing     | 43 mm
   Maximum height                        | 162.8 mm
   Maximum width                         | 148.6 mm
   Weight                                | 925 g              
   Grasp Force                           | 20 to 235 N                  
   Finger speed                          | 20 to 150 mm/s                   
   Maximum payload by grasp type         | 5 kg
   Form-fit grasp                        | 5 kg
   
## Change the USB device permissions 
1.View USB serial number
```bash
$ dmesg | grep ttyS*
```
2.View ttyUSB0 permissions
```bash
$ ls -al /dev/ttyUSB0
```
You can also manually change the permissions of the USB device with the chmod command, but the manual permission changes are only temporary. The USB device will restore its default permissions on the next reboot.

3.Change permissions to readable and writable
```bash
$ sudo chmod 777 /dev/ttyUSB0
```
Modify the permissions to be readable and writable executable, but this setting will still be restored after the computer restarts.


Note that Robotiq devices that use the USB serial port will appear as /dev/ttyUSBn devices in your system (where "n" is a number that depends on the number of USB devices that are plugged in the computer) and require read and write permissions to work properly. One way to permanently ensure you have such permissions is simply to add your user to the dialout group once:

4. Change to have permanent permissions and change USERNAME to your own username
```bash
$ sudo usermod -aG dialout $USERNAME
```
Add this username to the dialout user group, then log out of the computer. This will not modify the permissions for the next reboot.

To control the gripper over a serial port, you may need to give proper privileges to the user
```bash
$ usermod -a -G dialout YOURUSERNAME
```
To find out the port on which the controller is connected, use:
```bash
$ dmesg | grep tty
```
It's probably something like ttyUSB0.

## Installation
1. Create a new Robotiq workspace and download the robotiq package
```bash
$ mkdir -p robotiq_ws/src
$ cd robotiq_ws/src/
$ git clone https://github.com/ros-industrial/robotiq.git
$ cd ..
$ catkin_make
$ source devel/setup.bash
```

2.In the above workspace, install related dependencies
Modbus TCP:
```bash
$ rosdep install robotiq_modbus_rtu
```
The EtherCAT soem library is also required to build the Robotiq package. It can be downloaded from debs by
```bash
$ sudo apt-get install ros-kinetic-soem
```
## ROS Nodes to Control the Gripper
### Run the 2-Finger Gripper Driver Node
The gripper is driven by the node "Robotiq2FGripperRtuNode.py" contained in the package "robotiq_2f_gripper_control". Note that "roscore" should be running prior to launching the driver node. The gripper device ID will also need to be provided as an argument. Thus, to know what is the device ID of your 2-finger gripper, one way is simply by typing "dmesg | grep ttyUSB" in a terminal right after the gripper was connected to the computer's USB port.

For example, the driver for controlling a 2-finger gripper having "ttyUSB0" as its device ID is launched using the following command:
1.First to enter the ROS system:
```bash
$ roscore
```

2.Open a new terminal and run the 2-Finger gripper driver node
```bash
$ source devel/setup.bash
$ rosrun robotiq_2f_gripper_control Robotiq2FGripperRtuNode.py /dev/ttyUSB0
```
### Run the 2-Finger Gripper Simple Controller Node
The driver listens for messages on "Robotiq2FGripperRobotOutput" using the "Robotiq2FGripper_robot_output" msg type. The messages are interpreted and commands are sent to the gripper accordingly. A simple controller node is provided which can be run (in another terminal) using "rosrun robotiq_2f_gripper_control Robotiq2FGripperSimpleController.py"

Open a new terminal and run rRobotiq2FGripperSimpleController.py
```bash
$ source devel/setup.bash
$ rosrun robotiq_2f_gripper_control Robotiq2FGripperSimpleController.py
```
### Run the 2-Finger Gripper Status Listener Node
Open a new terminal and run Robotiq2FGripperStatusListener.py
```bash
$ source devel/setup.bash
$ rosrun robotiq_2f_gripper_control Robotiq2FGripperStatusListener.py
```

# reference :
 -USB Setting- 
 
 [1] Serial port permissions: https://blog.csdn.net/qq_28093585/article/details/78435876
 
 [2] Permanently modify USB device permissions: https://blog.csdn.net/weixin_40554881/article/details/84307491
 
 [3] Solution: Permanently have operational permissions: https://blog.csdn.net/w383117613/article/details/44216653
 
 [4] Modify USB device permissions: https://blog.csdn.net/jiangchao3392/article/details/76227180
 
 -Install & Run the ROS Node-
 
 [5] ROBOTIQ 3-Finger Adaptive Robot Gripper runtime environment:https://blog.csdn.net/w1301100424/article/details/88540442
 
 [6] Rotating the Robotiq 2f-140 electric claw in the Ros environment:https://blog.csdn.net/lingchen2348/article/details/82858376
 
 [7] ROS.org Robotiq Package Summary: http://wiki.ros.org/robotiq
 
 [8] Robotiq Tutorials Control of a 2-Finger Gripper using the Modbus RTU protocol (ros kinetic and newer releases):http://wiki.ros.org/robotiq/Tutorials/Control%20of%20a%202-Finger%20Gripper%20using%20the%20Modbus%20RTU%20protocol%20%28ros%20kinetic%20and%20newer%20releases%29#Run_the_2-Finger_Gripper_Simple_Controller_Node
 
 [9] What is this rosdep error ?: https://answers.ros.org/question/35741/what-is-this-rosdep-error/
 
 
 
