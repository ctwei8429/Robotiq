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

4. Change to have permanent permissions and change USERNAME to your own username
```bash
$ sudo usermod -aG　dialout $USERNAME
```
Add this username to the dialout user group, then log out of the computer. This will not modify the permissions for the next reboot.






# reference :
 -USB Setting- 
 
 [1] Serial port permissions: https://blog.csdn.net/qq_28093585/article/details/78435876
 
 [2] Permanently modify USB device permissions: https://blog.csdn.net/weixin_40554881/article/details/84307491
 
 [3] Solution: Permanently have operational permissions: https://blog.csdn.net/w383117613/article/details/44216653
 
 [4] Modify USB device permissions: https://blog.csdn.net/jiangchao3392/article/details/76227180
