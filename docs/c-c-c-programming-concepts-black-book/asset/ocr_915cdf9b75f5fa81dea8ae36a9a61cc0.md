To view the type metadata, we need to click the type information label. In our case, we have clicked the a : public static literal int32. A new window appears displaying the type metadata, as shown in Figure 16.13:

![](bbox=[0.322, 0.194, 0.702, 0.377])

# MSIL/CIL Information

MSIL code contains information, such as code size and data related to stack. To view the MSIL code for the Example.cs program, we need to click the “Main: void()” label. A new window appears that shows the MSIL code for the Example.cs program, as shown in Figure 16.14:

![](bbox=[0.322, 0.476, 0.702, 0.661])

# Resource File

Resource files in .NET are used to store the resources, such as bitmaps, icons, and local-specific strings. These files are created with an extension resx. When we compile the code in the .NET platform, the compiler compiles these files into the binary files with the .resource extension and then the linker put these files into the assembly. Therefore, the final .exe, which will be executed, contains the information about the resources as well. The resource files ease the job of the processor in managing the resources.

Let’s now discuss about Global Assembly Cache that has a huge importance in the study of the .NET architecture.