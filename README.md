# Camera mlx90640 overlay

Based on https://github.com/obstruse/ThermalCamera

The only difference is it works with 64 bit Raspberry Pi OS since it uses picamera2 instead of pygame.camera

* Connect to GPIO pins

* Enable I2C via raspi-config or Preferences - Raspberry Pi Configuration - Interfaces - I2C

```
i2cdetect -y -r 1
```

should result in

```
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- 33 -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- --
```

```
pip install adafruit-circuitpython-mlx90640
pip install pygame
pip install opencv-python
pip install picamera2
pip install -U numpy
pip install colour
```

Assure to use latest version of numpy

```
sudo apt-get install libatlas-base-dev
```

Start the script
```
python3 heat.py
```

### Working configuration

* Raspberry Pi 4
* MLX90640 (via GPIO pins)
* Official RPi display (via DSI)
* Official camera module v1.3 (via CSI)
* Evatronic PD Pioneer 20000mAh
    - USB C: RPi
    - Micro-USB: Display

### Attention to /boot/config.txt and reboot after making changes

* Add: dtparam=i2c1_baudrate=400000
* Set: camera_auto_detect = 0
* Set: dtoverlay=ov5647
* Keep dtoverlay=vc4-kms-v3d enabled
* Keep max_framebuffers=2 enabled

See also: https://www.raspberrypi.com/documentation/computers/camera_software.html
