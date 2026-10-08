For RackAFX have two options for starting a new project: download one of my sample projects or start a new project from scratch and develop it. Unlike VST3 and AU, starting a new project is simple and takes less than 30 seconds. I suggest starting each from scratch, but the projects are available if you prefer starting with code. There are a set of downloadable projects for each:

+   - GUI only—the GUI is already done for you and variables declared, but you have to do the rest, including adding the additional files for each project
- Full-whole project include; we don't recommend simply compiling someone's code as a learning method, having the full code allows you to not check your work but also step the code in debug mode so you can see how the client interacts-in short, the full projects are excellent for helping you debug and understand your projects-in-progress

Unlike VST3 and AU, RackAFX will create your project for you. Use the File->New Project or N to start a new project. A form allows you to enter the project name.

![](bbox=[0.237, 0.307, 0.762, 0.633])

Figure 2.6: The interfaces interface.

For the MiniSynth, you would start out with the New Dialog in Figure 2.7.

In this case, you name the project MiniSynth and check the Hungarian notation box in View->Preferences. RackAFX creates the Visual Studio project for you and copies all the code files you need. The Visual Studio project files will be packaged in a folder with your <Project Name>, in this case MiniSynth. The C++ object will be packaged in the files MiniSynth.h and MiniSynth.cpp. The object will be named MiniSynth. Make sure you check the "Only Output Synthesizer plug-in" and if you forget, you can always come back

The Project Name will be the name of your C++ class. So, you need to be careful about using a name that is a legal C++ object name. Also, if you check the Hungarian notation box in preferences, a "C" will be added to the name of your object.

change it File->Edit Project or the < Edit> button.

The synth projects in this book will require additional files—a that we provide and a bunch that you will write in the next few chapters. You will always need the synthfunctions.h, which you can get from the website. The other files