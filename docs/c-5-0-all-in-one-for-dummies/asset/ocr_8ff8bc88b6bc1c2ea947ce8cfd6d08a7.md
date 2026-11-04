Then you wait. Visual Studio is big. It takes a while.

The official requirements for Visual Studio are shown in this list:

+   - **Operating system:**
+     - Windows 7 SP1
+     - Windows 8
+     - Windows Server 2008 R2 SP1
+     - Windows Server 2012
+   - **Supported architectures:**
+     - 32-bit (x86)
+     - 64-bit (x64)
+   - **Hardware:**
+     - 1.6 GHz or faster processor
+     - 1GB of RAM
+     - 10GB of available hard disk space
+     - 5400 RPM drive
+     - DirectX 9-capable video card at 1024x768

You can run on this configuration — I have tried it, and it works. It’s not pretty. Visual Studio 2012 is all written in WPF, which can (with this size of an application) be a resource hog.

Seeing how that is the case, I am sure you aren’t surprised to find that I have a collection of suggestions for installing Visual Studio.

First, here is what I consider to be a realistic base configuration for Visual Studio:

+   - 2.4 GHz 64 bit dual core processor
+   - 64-bit Windows 8 with 8GB of RAM
+   - 250GB of available HDD space
+   - Dual monitors (or a laptop with an external monitor) with one being a touch screen

Seems excessive? It isn’t. First, I recommend that you use a virtual machine for any project that does anything to your base install of Windows. Virtual PC is free, and you can usually get a 180-day trial of Windows 8 without a problem. Change the settings on Virtual PC to run the clock only while the machine is running, and you have a perfect test bed.