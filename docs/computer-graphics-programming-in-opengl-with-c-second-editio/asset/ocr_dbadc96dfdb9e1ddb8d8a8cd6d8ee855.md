Simply run an existing program with Nsight enabled. Nsight allows examining shaders at runtime, such as seeing the current contents of a shader's uniform variables. Some versions even allow for changing the shader code at runtime.

There are versions of Nsight for Windows and for Linux/MacOS that can interact with Microsoft's Visual Studio (VS) and the Eclipse IDE. We restrict our discussion to Windows and Visual Studio. (In our "sister" book *Computer Graphics Programming in OpenGL with Java*, we describe using Nsight with Java-based programs.)

Nsight works only with compatible NVIDIA graphics cards; it won't work with Intel or AMD graphics cards. A complete list of supported cards is available on the NVIDIA website [NS20].

Nsight is changing quickly, and the description in our previous (first) edition of this textbook is already outdated. The reader should consider this brief introduction just a starting point, as there are likely to be many more exciting changes and developments in Nsight in the near future.

# ## 9.2 SETTING UP NSIGHT

There are various ways of setting up Nsight and incorporating it into Visual Studio. Depending on the version that you install, an Nsight menu will either be added to the topmost VS menu or as a sub-menu to the "Extensions" menu. We installed Nsight as follows:

+   1. Install NVIDIA **Nsight Graphics**, available at *https://developer.nvidia.com/nsight-graphics*. We installed version 2020.4.
+   2. In Visual Studio, use *Extensions ▶ Manage Extensions* to search for and install **Nsight Integration**. The "Nsight" menu should appear, either in the top menu bar or as a submenu under Extensions.

# ## 9.3 RUNNING A C++/OPENGL APPLICATION IN NSIGHT

+   1. Load the program that you wish to run, if you haven't done so already. In the "Nsight" menu, run your program by choosing "Frame Debugger" or "Start Graphics Debugging" (depending on your version and installation), as shown here: