# Brokers

AppContainer processes have almost no permissions except for those implicitly granted with capabilities, some common operations cannot be performed by the AppContainer and require help. (There are also too level to be visible to users in the store, and difficult to manage.) Some examples include selecting files using the common Open dialog box or printing a Print dialog for these and other operations, Windows provides helper processes, called brokers, managed by the system process, RuntimeBroker.exe.

An AppContainer requires that any of these communicates with the Runtime Broker through a secure ALPC channel and Runtime Broker initiates the creation of the requested broker process. Examples are %SystemRoot%\PrintDialog\PrintDialog.exe and %SystemRoot%\System32\PickerHost.exe.

# EXPERIMENT: Brokers

The following steps show how broker processes are launched and terminated:

+   1. Click the Start button, type Photos, and select the Photos to run the built-in Windows 10 Photos application.
2. Open Process Explorer, switch the process to a tree view, and locate the Microsoft Photos.exe process. Place both windows side by side.
3. In the Photos app, select a picture file, and click Print in the top ellipsis menu or right-click the picture and choose Print from the menu that appears. The Print dialog box should open, and Process Explorer should show the newly created broker (PrintDialog.exe). They are all children of the same svchost process. (All UWP processes are launched by the DCOML hosting service installed by this process.)

![](bbox=[0.233, 0.574, 0.766, 0.893])

+   4. Click the Print dialog box. The PrintDialog.exe process should exit.

CHAPTER 7 Security 709