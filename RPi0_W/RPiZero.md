# Raspberry Pi Zero W

You will have to solder the pins on to the board yourself, [Nolop](https://nolop.org/solder/) has access to several soldering stations. To interface with the Servo Hat, solder [MALE Pin headers](../public/male-pin-headers.jpg) to your board.

## Getting Started

1. Plug your SD Card into the Raspberry Pi
2. Connect your peripherals to the Raspberry Pi Zero W
   * Plug the power cable in last
   * The EPDC located in the SEC has computers, physically re-route the peripherals from one of the computers there to your Raspberry Pi Zero 
3. Wait - This part may take a bit of time, if it takes longer than 10 minutes. Disconnect the power cable and then reconnect
4. Follow the instructions in the dialog box, keeping the following in mind if you plan on connect to WiFi on Tufts Campus...
    * Connect to Tufts_Wireless
    * Don't Check for Updates (It won't work as there is one more step to connect to the internet)
    * Type `ifconfig wlan0` into the terminal window to find the MAC Address of your Raspberry Pi and register it with Tufts Technology Services via the online form.
5. Configure the following interface(s):
    * I2C (For Controlling the [Servo Hat](https://www.waveshare.com/wiki/Servo_Driver_HAT))
    * Serial (Optional)
    * VNC (Optional)
    * SSH (Optional)
    * Type `sudo raspi-config` into the command line and navigate to *3 Interface Options*
6. Update the packages on your Raspberry Pi by opening a Terminal Window and entering the following line... `sudo apt update -y && sudo apt-get update -y && sudo apt-get upgrade -y`
7. `sudo reboot`

![Diagram of Peripheral Connections](./RPIconnectionDiagram.svg)

## Getting Started [Without a Monitor](https://howchoo.com/pi/raspberry-pi-gadget-mode)

1. Flash Raspberry PI OS onto your [SD Card](https://howchoo.com/pi/install-raspberry-pi-os)
2. Edit config.txt on the boot partition and append `dtoverlay=dwc2`
3. Enable SSH, on the command line in the boot directory type `touch ssh`
4. Edit `cmdline.txt` Look for `rootwait`, and add `modules-load=dwc2,g_ether` immediately after. Save and Exit
5. Connect over USB and boot the Pi
6. Follow the above instructions starting at 4.

## USING the Raspberry Pi Without a Monitor

1. First complete one of the getting started paths described above.
2. SSH MUST be enabled on your Raspberry Pi
3. Connect your computer to the same WiFi as your Pi.
4. Find the IP Address of your Pi on your local WiFi (On Tufts Wireless go to your Device Registration)
   * From the Pi, run `ifconfig` again and get the IP address
5. From your computer you can now *SSH Into Your Pi*
    * `ssh -l pi@<Your Pi???s IP Address>`

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

4. Connect the hat to the top of the Raspberry Pi Zero
5. Connect one or more servos to the hat, using the following diagram.
   * **Every time you connect a servo to the Raspberry Pi it will restart**
   * The LiPo Battery Pack is only necessary if you want to operate without connecting the Raspberry Pi to power.
   * In order to make a connection between the LiPo and green Terminal I soldered two jumper cables to the end of the connector provided to you.
![Wiring Servo to RPI0](./WaveShareServoHat.svg)
![Soldered Connection](./LiPo/solderedConnector.jpg)
6. The LiPo Battery Pack is only necessary if you want to operate without connecting the Raspberry Pi to power.
    *	To make a connection between the LiPo and green terminal I soldered two jumper cables to the end of the connector.
    *	When attaching your LiPo Battery to the Waveshare Servo Hat make sure the Red wire attaches to VIN and the Black Wire Attaches to GND
    *	CAUTION: IF USING THE LIPO BATTERY SEE THE SECTION ON SAFETY PROCEDURES AT THE END OF THIS SHEET

## Getting Readings from the [Lidar Sensor](https://learn.adafruit.com/adafruit-vl53l0x-micro-lidar-distance-sensor-breakout/python-circuitpython)

1. pip install the `adafruit-circuitpython-vl53l0x` package

        sudo pip3 install adafruit-circuitpython-vl53l0x
2. To get reading import the adafruit_vl53l0x package and use the following commands

    ```python
      import board, busio, adafruit_vl53l0x

      # Initialize I2C bus and sensor.
      i2c = busio.I2C(board.SCL, board.SDA)
      sensor = adafruit_vl53l0x.VL53L0X(i2c)

      # Get Data
      sensor.range
    ```

3. Wiring Diagram
   * Pi 3V3 to sensor VIN (red wire on STEMMA QT version)
   * Pi GND to sensor GND (black wire on STEMMA QT version)
   * Pi SCL to sensor SCL (yellow wire on STEMMA QT version)
   * Pi SDA to sensor SDA (blue wire on STEMMA QT version)

![Wiring Lidar to RPI0](./RPI0LidarWiring_bb.svg)

## Getting Readings from the Ultrasonic Sensor

Like with the ESP32, there is no specific package used to manage the Ultrasonic Sensor HC-SR04. Instead you should wire it up as shown below and look for example code on the [internet](https://pimylifeup.com/raspberry-pi-distance-sensor/)!

* VCC Connects to Pin 2 (5v)
* Trig Connects to Pin 7 (GPIO 4)
* Echo Connects to R1 (1k ???)
* R2 (2k ???) Connects from R1 to Ground
* Wire from R1 and R2 connects to Pin 11
* GND connects to Pin 6 (Ground)

![Wiring HC-SR04 to RPI0](./RPI0UltrasonicWiring_bb.svg)

## Getting Readings from the IMU [(MPU9250)](https://makersportal.com/blog/2019/11/11/raspberry-pi-python-accelerometer-gyroscope-magnetometer)

## Getting Started with the Camera

### [Simple Pictures and Videos](https://projects.raspberrypi.org/en/projects/getting-started-with-picamera)

1. First make sure that the camera interface is enabled by typing, `sudo raspi-config` then select  **3 Interface Options**
2. Locate the Camera Module port
3. Gently pull up on the edges of the port???s plastic clip
4. Insert the Camera Module ribbon cable; make sure the connectors at the bottom of the ribbon cable are facing the contacts in the port.
5. Push the plastic clip back into place
6. Then try to get an image by typing

        $ raspistill -o Desktop/image.jpg

7. Now record a video with the Camera Module by using the following raspivid command:

        $ raspivid -o Desktop/video.h264

### [Getting OpenCV](https://www.pyimagesearch.com/2015/03/30/accessing-the-raspberry-pi-camera-with-opencv-and-python/)

1. Next you want to install some dependencies

        $ sudo apt-get update && sudo apt-get upgrade
        $ sudo apt-get install libhdf5-dev
        $ sudo apt-get install libatlas-base-dev
        $ sudo apt-get install libjasper-dev 
        $ sudo apt-get install libqtgui4 
        $ sudo apt-get install libqt4-tes


2. Now pip install opencv

        $ sudo apt-get install python3-opencv

3. Now to use the library you can `import cv2` in a python file. For AI detection of face, bodies, etc. use *haarcascade*.

## Important Links and Information (RPi Zero W)

* [Amazon Link](https://www.amazon.com/Vilros-Raspberry-Starter-Power-Premium/dp/B0748MPQT4)
* [YouTube Tutorial](https://www.youtube.com/watch?v=Hdm26W9dHK0)
* [Setup Page](https://maker.pro/raspberry-pi/tutorial/how-to-get-started-with-the-raspberry-pi-zero-w)
* My Kit did not come with headers for the Raspberry Pi [Same in Reviews](https://www.amazon.com/Vilros-Raspberry-Kit-Premium-Essential-Accessories/dp/B0748NK116/ref=sr_1_5?crid=1KENGVI6UOIVY&dchild=1&keywords=pi+zero+w+kit&qid=1630359207&s=electronics&sprefix=pi+zero+w%2Celectronics%2C184&sr=1-5)
* [Using the Servo Motor](https://www.waveshare.com/w/upload/1/1b/Servo_Driver_HAT_User_Manual_EN.pdf)
* [Getting Readings from Lidar Sensor](https://learn.adafruit.com/adafruit-vl53l0x-micro-lidar-distance-sensor-breakout/python-circuitpython)
<!-- * [Datasheet of Lidar](https://cdn-learn.adafruit.com/assets/assets/000/037/547/original/en.DM00279086.pdf) -->
* [Getting Readings from the Ultrasonic Sensor](https://pimylifeup.com/raspberry-pi-distance-sensor/)
<!-- * [Datasheet of Ultrasonic Sensor](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf) -->

[![Raspberry Pi Zero Pinout](./raspberry-pi-pinout.png)](https://pinout.xyz/)
