# Figure 3.9: The preferences interface.

In the preferences you need to:

+   1. Choose your default folders for projects, WAVE files, and default WAVE files. You can use whatever directory you want for your project folder and you can also open projects from any other folder at any time; the default is simply for conveniently grouping all your projects together.
+   2. Choose a Visual C++ compiler.
+   3. Set the C++ options. Enable C++ Control/Switching should be left on for all but the most advanced users. C++ control/switching allows RackAFX to control Visual Studio, save files, launch the debugger, and so on.
+   4. Set up the edit options when entering information in the GUI slider/button dialogs.

# 3.9.1 Project: Volume

Create a new project with the menu, toolbar, or Ctrl+N and name it “Volume.” The New/Edit Project window will appear and you can enter your project name. As you enter the name, the .h and .cpp files will be automatically named.

Notice the two C++ files listed in Figure 3.10—these are the interface (.h) and implementation (.cpp) files that RackAFX will create for you. They will contain a derived object named CVolume which will contain the bulk of your plug-in code. When you hit OK, several things happen. If you have C++ Control enabled in your preferences (it’s the default) then you will see your C++ compiler start up. In Visual C++ you will see a new project and solution named “Volume.” If you expand the Volume project then you can see the files that RackAFX wrote for you. Your derived class is contained in Volume.h and Volume.cpp. Before continuing, it’s worth taking a peek into the RackAFXDLL.cpp file and locating the creation mechanism createObject():

![](bbox=[0.27, 0.6, 0.72, 0.8])

# Figure 3.10: The top section of the New/Edit Project window. Notice that your project name becomes the name of a C++ object, so you will receive errors if you name the project in a way that produces illegal C++ syntax. Below this are more advanced settings that we will cover later.