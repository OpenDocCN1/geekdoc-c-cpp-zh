
You will need to enable SSH. The steps are as follows:

- Start the configuration tool:

```
pi@raspberrypi:~$ sudo raspi-config
```

- Move down to **Interface Options** and select **SSH** and enable it.
- If you are in GUI mode, click the Wi-Fi icon at the top right hand of the screen and enable Wi-Fi. Note the IP address allocated automatically to your Raspberry Pi.
- You can now remotely access your Raspberry Pi using terminal emulation software, such as **Putty** (see Section 1.4 and 1.5).

## 1.3 • Using networked connection

If you do not have a suitable monitor and keyboard to directly connect to your Raspberry Pi, you will have to use a networked connection and remotely access your Raspberry Pi using a PC. There are two options: **connection using an Ethernet cable**, and **connection over Wi-Fi**.

**Connection using an Ethernet cable:** The steps are as follows:

- Install **Notepad++** on your PC from the following web site:

https://notepad-plus-plus.org/downloads/v7.8.5/

- Insert the SD card back to your PC and start **Notepad++**.
- Click **Edit -> EOL Conversion -> UNIX/OS X Format**.
- Create a new empty file with the **Notepad++** and save it to the boot folder of the SD card with the name **ssh** (without any extension), where this file will enable SSH to be used to remotely access your Raspberry Pi. In Windows, this is the only folder you will see which contains items including loader.bin, start.elf, kernel.img, etc.
- Insert the SD card back into your Raspberry Pi.
- Connect your Raspberry Pi to one of the ports of your Wi-Fi router through an Ethernet cable and power it up.
- Find out the IP address allocated to your Raspberry Pi by accessing your Wi-Fi router. Alternatively, install **Advanced IP Scanner** on your PC, which is available at the following link:

https://www.advanced-ip-scanner.com

- Run the software and look for your Raspberry Pi. You do not have to install the software to run it. Click **Run portable version**, and then **Scan**. As shown in Figure 1.5, the IP address of the author’s Raspberry Pi was 192.168.1.202.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_13_0.png)

- You can now use Putty to log in to your Raspberry Pi (see Section 1.4 and 1.5)

Alternatively, you can find the IP address of your Raspberry Pi by opening the command prompt on your PC with administrator privilege (by right-clicking to accept to run as an administrator) and then inputting the command: `ping raspberrypi.home` as shown in Figure 1.6.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_14_0.png)

It is also possible to find the IP address of your Raspberry Pi using your smartphone. Many apps can be used to find out who is currently using your Wi-Fi router. e.g. **Who's On My Wi-Fi – Network Scanner** by Magdalm.

**Connection using Wi-Fi:** This is the preferred method to access your Raspberry Pi and is the one used by the author. Here, as described in Chapter 1, the Raspberry Pi can be placed anywhere you like within the range of the Wi-Fi router and is easily accessed from your PC using Putty (see Section 1.4 and 1.5).

The steps are:

- Install **Notepad++** on your PC from the following web site:
https://notepad-plus-plus.org/downloads/v7.8.5/
- Insert the SD card back to your PC and start **Notepad++**.
- Click **Edit -> EOL Conversion -> UNIX/OS X Format**
- Create a new empty file with **Notepad++** and save it to the boot folder of the SD card with the name `ssh`(without any extension), where this file will enable SSH to be used to remotely access your Raspberry Pi. In Windows, this is the only folder you will see which contains items like loader.bin, start.elf, kernel.img, etc.
- Enter the following statements into a blank file (replace the **MySSID** and **MyPassword** with the details of your own Wi-Fi router):

```
country=GB
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
    scan_ssid=1
    ssid="MySSID"
    psk="MyPassword"
}
```

- Copy the file (save) to the boot folder on your SD card with the name: **wpa_supplicant.conf**.
- Insert the SD card back into your Raspberry Pi and power-up the device.
- Use **Advanced Ip Scanner** or one of the methods described earlier to find out the IP address of your Raspberry Pi.
- Log in to your Raspberry Pi remotely using **Putty** on your PC (see Section 1.3 and 1.4).
- After logging in, you are advised to change your password for security reasons. You should also run **sudo raspi-config** from the command line to enable VNC, I2C, and SPI as they are useful interface tools that can be used in your future GPIO based work.

## 1.4 • Remote access

It is much easier to remotely access the Raspberry Pi over the internet: for example using a PC rather than connecting a keyboard, mouse, and display to it. Before being able to remotely access the Raspberry Pi, we have to enable SSH by entering the following command in a terminal session (if you have followed the steps given earlier, SSH is already enabled and you can skip the following command):

```
pi@raspberrypi:~$  sudo raspi-config
```

Go to the configuration menu and select **Interface Options**. Go down to **P2 SSH** and enable SSH. Click **<Finish>** to exit the menu.

You should also enable VNC so the Raspberry Pi Desktop can be accessed graphically over the internet. This can be done by entering the following command in a terminal session:

```
pi@raspberrypi:~$  sudo raspi-config
```

Go to the configuration menu and select **Interface Options**. Go down to **P3 VNC** and enable VNC. Click **<Finish>** to exit the menu. At this stage you may want to shut down or restart your Raspberry Pi by entering one of the following commands in command mode:

```
pi@raspberrypi:~$  sudo shutdown now
```

or

```
pi@raspberrypi:~$  sudo reboot
```

## 1.5 • Using Putty

Putty is a communications program used to create a connection between your PC and Raspberry Pi. This connection uses a secure protocol called SSH (Secure Shell). Putty doesn’t need to be installed and can be stored in any folder of your choice and run from there.

Putty can be downloaded from the following web site:

[https://www.putty.org/](https://www.putty.org/)

Simply double click to run it and the Putty startup screen will be displayed. Click **SSH** and enter the Raspberry Pi IP address, then click **Open** (see Figure 1.7). The message shown in Figure 1.8 will be displayed the first time you access the Raspberry Pi. Click **Yes** to accept this security alert.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_16_0.png)

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_17_0.png)

Figure 1.8 Click Yes to accept

You will be prompted to enter the username and password. Notice the default username and password are:

username: pi
password: raspberry

You now have a terminal connection with the Raspberry Pi and can type in commands, including the sudo privileged administrative commands.

To change your password, enter the following command:

```
passwd
```

You can use the cursor keys to scroll up and down through the commands you’ve previously entered in the same session. You can also run programs although not graphical programs.

### 1.5.1 ● Configuring Putty

By default, the Putty screen background is black with white foreground characters. The author prefers to have white background with black foreground characters, with the character size set to 12 points bold. The steps to configure the Putty with these settings are given below. Notice that in this example these settings are saved with the name RPI4 so that they can be recalled whenever the Putty is restarted:

- Restart Putty.
- Select SSH and enter the Raspberry Pi IP address.
- Click Colours under Window.
- Set the Default Foreground and Default Bold Foreground colours to black (Red:0, Green:0, Blue:0).
- Set the **Default Background** and **Default Bold Background** to white (Red:255, Green:255, Blue:255).
- Set the **Cursor Text** and **Cursor Colour** to black (Red:0, Green:0, Blue:0).
- Select **Appearance** under **Window** and click **Change** in **Font settings**. Set the font to **Bold 11**.
- Select **Session** and give a name to the session (e.g. RPI4) and click **Save**.
- Click **Open** to open the Putty session with the saved configuration.
- Next time you re-start the Putty, select the saved session and click **Load** followed by **Open** to start a session with the saved configuration.

## 1.6 ● Remote access of the Desktop

You can control your Raspberry Pi via Putty, and run programs on it from your Windows PC. This however will not work with graphical programs because Windows doesn't know how to represent the display. As a result of this, for example, we cannot run any graphical programs in the Desktop mode. We can get round this problem using some extra software. Two popular software used for this purpose are: VNC (Virtual Network Connection), and Xming. Here, we shall be learning how to use the VNC.

### Installing and using VNC

VNC consists of two parts: VNC Server and the VNC Viewer. VNC Server runs on the Raspberry Pi, and the VNC Viewer runs on the PC. VNC server is already installed on your Raspberry Pi and is enabled as described in Section 1.3 using raspi-config.

The steps to install and use VNC Viewer on your PC are given below:

- There are many VNC Viewers available, but the recommended one is TightVNC which can be downloaded from the following web site:
https://www.tightvnc.com/download.php
- Download and install **TightVNC** for your PC. You will have to choose a password during the installation.
- Enter the following command:
```
pi@raspberrypi:~$ vncserver :1
```
- Start **TightVNC Viewer** on your PC and enter the Raspberry Pi IP address (see Figure 1.9) followed by :1. Click **Connect** to connect to your Raspberry Pi.
