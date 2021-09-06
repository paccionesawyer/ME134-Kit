# Raspberry Pi Zero W

## Getting Started

1. Plug your SD Card into the Raspberry Pi
2. Connect your peripherals to the Raspberry Pi Zero W ![Diagram of Peripheral Connections](./public/newDiagram.svg)
   * Plug the power cable in last
3. Wait - This part may take a bit of time, if it takes longer than 10 minutes. Disconnect the power cable and then reconnect
4. Follow the instructions in the dialog box, keeping the following in mind if you plan on connect to WiFi on Tufts Campus...
    * Connect to Tufts_Wireless
    * Don't Check for Updates (It won't work as there is one more step to connect to the internet)
    * Find the MAC Address of your Raspberry Pi and register it with Tufts Technology Services via the online Form
5. Configure the following interface(s):
    * I2C (For Controlling the [Servo Hat](https://www.waveshare.com/wiki/Servo_Driver_HAT))
    * Serial (Optional)
    * VNC (Optional)
    * SI : Type `sudo raspi-config` into the command line and navigate to *3 Interface Options*
6. Update the packages on your Raspberry Pi by opening a Terminal Window and entering the following line... `sudo apt update -y && sudo apt-get update -y && sudo apt-get upgrade -y`
7. `sudo reboot`

## Using the [Waveshare Servo Hat](https://www.waveshare.com/w/upload/1/1b/Servo_Driver_HAT_User_Manual_EN.pdf)

1. I2C should be enabled (see **Getting Started** Number 5)
2. Install the following libraries from the Terminal Window
    * Using `sudo apt-get`
      * `update`, `sudo apt-get upgrade`, `install python-pip `, `install python-smbus`, `install p7zip-full`
    * Using `pip install`
      * `RPi.GPIO`
3. Download example files

        sudo apt-get install p7zip-full
        wget http://www.waveshare.net/w/upload/6/6c/Servo_Driver_HAT.7z
        7zr x Servo_Driver_HAT.7z -r -o./Servo_Driver_HAT
        sudo chmod 777 -R Servo_Driver_HAT
        cd Servo_Driver_HAT/Raspberry\ Pi/

## Important Links and Information (RPi Zero W)

* [Amazon Link](https://www.amazon.com/Vilros-Raspberry-Starter-Power-Premium/dp/B0748MPQT4)
* [YouTube Tutorial](https://www.youtube.com/watch?v=Hdm26W9dHK0)
* [Setup Page](https://maker.pro/raspberry-pi/tutorial/how-to-get-started-with-the-raspberry-pi-zero-w)
* My Kit did not come with headers for the Raspberry Pi [Same in Reviews](https://www.amazon.com/Vilros-Raspberry-Kit-Premium-Essential-Accessories/dp/B0748NK116/ref=sr_1_5?crid=1KENGVI6UOIVY&dchild=1&keywords=pi+zero+w+kit&qid=1630359207&s=electronics&sprefix=pi+zero+w%2Celectronics%2C184&sr=1-5)

[![Raspberry Pi Zero Pinout](./public/raspberry-pi-pinout.png)](https://pinout.xyz/)
