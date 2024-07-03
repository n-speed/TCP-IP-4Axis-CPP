# Note: The below ReadMe is based on the original Dobot TCP-IP-MG400-CPP documenation

# 1\. Introduction

**TCP-IP-MG400-CPP** is a software development kit designed by Dobot based on the C language of TCP/IP protocol. It is developed based on C/C language, follows the Dobot-TCPIP control communication protocol, connects to the device terminal via Socket, and provides users with an easy-to-use API interface. Through TCP-IP-MG400-CPP, users can quickly connect to the Dobot device and carry out secondary development to control and use the device.

TCP-IP-MG400-CPP contains

1. api and CPPdemo. The api directory contains various classes that encapsulate the related functions of MG400/M1Pro, which are written based on C++.

2. cppdemo contains Windows/Linux examples as well as ROS examples.

3. [api/rapidjson](https://github.com/Tencent/rapidjson) is Tencent’s open source json parsing library.

## Pre-dependency

* Ubuntu 14.04/Ubuntu 16.04/Ubuntu 18.04, x86 and ARM (Nvidia TX2)

* Windows 10/11, Visual Studio 2015 Update3/2017/2019

* C++11 compiler
  
  This Demo is applicable to V1.5.6.0 and above controller version of MG400/M1Pro series.

## Version and Release

### Current version

| Version| Date|
|:----------:|:----------:|
| V1.0.0.0| 2023-03-07 |

# 2\. TCP-IP-MG400-CPP control protocol

As the communication based on TCP/IP has high reliability, strong practicability and high performance with low cost, many industrial automation projects have a wide demand for controlling robots based on TCP/IP protocol. Therefore, the MG400/M1Pro robot is designed to provide rich interfaces for interaction with external devices based on the TCP/IP protocol. For more details, see [TCP_IP Remote Control Interface Guide](https://github.com/Dobot-Arm/TCP-IP-Protocol.git).
 

## 3\. File and class descriptions

1. The api directory contains various classes that encapsulate the related functions of MG400/M1Pro, which are written based on C++.

2. [api/rapidjson](https://github.com/Tencent/rapidjson) is Tencent’s open source json parsing library.

3. Class descriptions in the api directory:
  
   | Parameter| Default Value|
   |----------|----------|
   | BitConverter| Encapsulates the conversion of bytes to underlying types|
   | DescartesPoint| Encapsulation of Cartesian coordinate structure|
   | JointPoint| Encapsulation of joint point coordinate structure|
   | FeedbackData| Encapsulation of feedback data structure|
   | ErrorInfoBean| Encapsulation of error message|
   | ErrorInfoHelper| Error message helper class|
   | DobotClient| Interface class based on TCP communication, encapsulates the basic business of communication|
   | Dashboard| Derived from DobotClient, it implements the specific basic functions of the robot|
   | DobotMov| Derived from DobotClient, it implements the specific motion functions of the robot|
   | Feedback| Derived from DobotClient, it implements the specific feedback services of the robot|
   | | |


4. `alarm_controller.json`: Warning alarm profile, `alarm_servo.json`: Servo alarm profile.

5. `Form.h`,`Form.cpp`,`Form.ui`,`main.cpp`,`CppDemo.pro`: The UI implemented based on Qt.

**CDobotClient**

Interface class based on TCP communication, encapsulates the basic business of communication.

```c++
    class CDobotClient
    {
    public:
     }
```

**Dashboard**

Derived from DobotClient, it can deliver some settings-related commands to the robot. It implements the specific basic functions of the robot.

```c++
 class CDashboard : public CDobotClient
    {
    public:
     }
```

**DobotMove**

Derived from DobotClient, it can deliver some motion-related commands to the robot. It implements the specific motion functions of the robot.

```c++
  class CDobotMove : public CDobotClient
    {
    public:
  }    
```

**Feedback**

Derived from DobotClient, it implements the specific feedback services of the robot can can provide real-time feedback on robot status information.

```c++
    class CFeedbackData
    {
    public:
    };
```

**For details, see the PythonExample.py and the Demo example.**

# 4\. Common Problems

**Problem 1:**  TCP connection. Port 29999/30003 cannot be connected or cannot deliver commands after connecting.

**Solution:**  If the controller version is below V1.6.0.0, you can try to upgrade the controller to V1.6.0.0 or above. If the controller version is already V1.6.0.0 or above, you can feedback the problem to technical support.

**Problem 2:** During TCP connection, the 29999 control port can send commands, but the 30003 motion port cannot send commands.

**Solution:**  If motion queue is blocked, you can try to reopen the queue by delivering **clearerror()** and **continue()** commands via port 29999.

# 5\. Example

* Dobot-Demo realizes TCP control of the robot and other interactions. It connects to the control port, motion port, and feedback port of the robot respectively. It delivers motion commands to robot, and handles the abnormal status of the robot, etc.

1. Main thread: Connect to the control port, motion port, and feedback port of the robot respectively. Enable the robot.

2. Feedback status thread: Real-time feedback of robot status information.

3. Robot motion thread: Deliver motion commands to robot.

4. Exception handling thread: Judge and handle the abnormal status of the robot.

**Steps to run the Demo:**

***Before testing any robotic arm movement, make sure the area surrounding the robot is clear of obstacles and other objects to avoid collision. Failure to do so can result in property damage, injury, and/or damage to the robotic arm and its end effectors***

1. Connect to the robot via LAN1 interface, and set the local IP address to 192.168.1.X.
  
   Control Panel >> Network and Internet >> Network Connections.
   
   Select the connected Ethernet >> Right click >> Properties >> Internet Protocol Version (TCP/IPV4).
   
   Modify the IP address to 192.168.1.X.
   

2. Open the DobotStudio Pro, connect to the robot, and set the robot mode to **TCP/IP secondary development**.

3. Run program

   1. Enter the directory >> TCP-IP-4Axis-CPP/CppDemo/ folder to compile the Demo program.

   ```bash
   cd   TCP-IP-CR-CPP/CppDemo/
   bash compileDemo.sh
   ```

   2. Run the Demo.

   ```bash
   bash runDemo.sh
   ```

**Common problems**

**Problem 1**: Make sure the robot is in TCP/IP mode

**Problem 2**: Confirm the Cartesian coordinates of the different models (MG400/M1pro) in the Demo