# ### 13.9 File handling

pigpio supports the following file handling operations (for details see: http://abyz.me.uk/rpi/pigpio/cif.html#fileOpen ).

+   - File opening.
+   - File closing.
+   - Read bytes from a file.
+   - Write bytes to a file.
+   - Seek a position within a file.
+   - List file that matches a pattern.

# ### 13.10 Waves

pigpio supports many functions for creating and manipulating waveforms (for details see: http://abyz.me.uk/rpi/pigpio/cif.html#gpioWaveClear ).

# ### 13.11 piscope

pigpio supports a logic analyser that can be used to show the state of selected GPIO pins in real-time (for details see: http://abyz.me.uk/rpi/pigpio/piscope.html). The steps to install piscope are:

```
```
pi@raspberrypi:~$ sudo pigpiod
pi@raspberrypi:~$ wget abyz.me.uk/rpi/pigpio/piscope.tar
pi@raspberrypi:~$ tar xvf piscope.tar
pi@raspberrypi:~$ cd PISCOPE
pi@raspberrypi:~/PISCOPE make hf
pi@raspberrypi:~/PISCOPE make install
```
```

Make sure you are in desktop mode of your Raspberry Pi (if you are using SSH, start a desktop session using a VNCServer/VNCViewer session. Open a terminal session in desktop mode, and start piscope to run in the background:

```
```
pi@raspberrypi:~$ piscope&
```
```

You should see a display as in Figure 13.9 which shows the state of each pin in real-time. You can use the arrow keys to change the time scale of the display. Samples can be saved if required. In Figure 13.9, pin GPIO 2 (or SDA) was toggled a few times and this is clearly shown on the display.