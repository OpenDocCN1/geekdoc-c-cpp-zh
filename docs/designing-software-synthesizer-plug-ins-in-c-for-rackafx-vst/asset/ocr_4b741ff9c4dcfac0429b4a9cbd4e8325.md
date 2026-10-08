the joystick has its colors altered, and you can set the program button to look like the assignable buttons—there can be only one joystick

you can add any continuous control (slider) to the GUI LCD group; it is a separate entity from the one on your main RackAFX GUI

when you add radio button controls, RackAFX starts with the topmost bank on the main GUI and automatically links your control variable. It moves from top to bottom as you drag the buttons. If you need to skip button banks, all of them at first, then reorder the ones you don't. The buttons are highly customizable.

the RackAFX GUI is constantly being designed so the control images and orders are steadily improved which means that your version of the software may not exactly resemble the figures here. Be sure to check the website http://www.willpark.com/synthbook/ for updates and on how to use the most recent version of the GUI.

For the synths in this book, we will not use the meter or assignable button controls. If you want to learn how to use these, see Designing Audio Effects Plug-Ins in C++, which several projects will feature these controls.

# Compiling as VST2/VST3 Plug-in

Once your plug-in is compiled, and you've added a GUI with the GUI Designer, you can go back to the project setup using File->Edit Project or the Edit button on the right. Here you can select "Make VST2 Compatible" and "Use RackAFX Custom GUI". When you say OK, it will take some time, as RackAFX copies over some files and re-configures your Visual Studio files. Once complete, rebuild the project. The DLL can be found by using the menu Item->Open Plugins the VST folder of any VST2 client and used as other plug-in. You can also copy this DLL and change the extension to .vst and place it in the VST3 folder of any VST2 client to use the DLL as a VST3 plug-in. The GUI you designed will appear as the custom GUI in the VST2 and VST3 clients.

_stdcall

In the RackAFX code you will see the qualifier _stdcall preceding each function prototype as implementation. The _stdcall calling convention is for future compatibility with other compilers as well as any 3rd party software. The _stdcall is a directive that tells the compiler how the stack is cleaned up after method calls; it has no effect on the math or audio processing thread.

# 2.14 The RackAFX Plug-in Object

Now that you know how to set up a GUI and the GUI Designer, let's focus on the synth plug-in object itself. We need to look at an example that shows how the functions in Tables 2.2 and 2.3 are implemented. After setting up the prototype GUI, your next job will be filling in the various functions that implement the plug-in according to Tables 2.2 and 2.3. Remember, you need to fill in ten functions any others you add to make a completed plug-in, so let's look those functions. Also remember that RackAFX project names are actually the plug-in C++ object name, each synth will be implemented as a different plug-object.

+   - download the MiniSynth and open it in RackAFX by using the File->Open button on the right.

+   - place the MiniSynth in the RackAFX Projects folder you selected in View->Preferences (you can always change it).

+   - RackAFX projects can be located in any folder except the desktop or a virtual drive but RackAFX will first default to the directory you choose in preferences.

+   - browse to find the MiniSynth.prj file and open it; the compiler will start.