# STM32-ROS-ExpansionBoard

This repository provides the STM32 setup files and instructions necessary for integrating STM32 with Ubuntu using Yahboom's hardware.

## Overview

These instructions cover the STM32 setup for communication with Python. The setup process is based on resources provided by Yahboom, with modifications for improved clarity and usability.

## Installation

1. **Install Required Dependencies**
    ```
    sudo apt update && sudo apt install python3-pip nano -y

2. **Install the STM32 Library**
    ```
    git clone https://github.com/TheTacoBytes/STM32-ROS-ExpansionBoard .
  
    cd py_install
  
    sudo python3 setup.py install
    ```

3. **Set Up USB Serial Permissions**
   - Go to the `rules.d` directory:
    ```
    cd /etc/udev/rules.d/
    ```
    
   - Create and configure the `usb_serial.rules` file for permissions:
    ```
    sudo touch usb_serial.rules

    sudo chmod 777 usb_serial.rules
    ```

   - Edit `usb_serial.rules` to include necessary USB permissions:

    ```
    sudo nano usb_serial.rules
    ```
    
   - Add the following:
    ```
    
    KERNEL=="ttyUSB*", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", MODE:="0777", SYMLINK+="myserial"
    KERNEL=="ttyUSB*", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", MODE:="0777", SYMLINK+="rplidar"
    ```

5. **Apply Changes**
   ```
   sudo udevadm trigger
 
   sudo service udev reload
   
   sudo service udev restart
   ```
   After running these commands, you will need to reconnect the STM32 board for the changes to take effect on.


## Acknowledgments

This STM32 setup is based on initial setup instructions from [Yahboom’s ROS Robot Expansion Board project](https://github.com/YahboomTechnology/ROS-robot-expansion-board). For the original resources, please refer to their official documentation.
