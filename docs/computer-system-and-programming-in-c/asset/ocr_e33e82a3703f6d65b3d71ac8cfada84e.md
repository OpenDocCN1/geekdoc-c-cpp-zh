+   c. **SQLite:** SQLite is the database engine used in android for data storage purposes.
+   
+    d. **WebKit:** It is the browser engine used to display HTML content.
+   
+    e. **OpenGL:** Used to render 2D or 3D graphics content to the screen.

+   - **Location Manager:** Location management, using GPS or cell tower.
+   - **Resource Manager:** Manage the various types of resources we use in our application.

# c. *Android Runtime*

Android Runtime consists of Dalvik Virtual machine and Core Java libraries.

+   a. **Dalvik virtual machine:** It is a type of JVM used in android devices to run applications and is optimized for low processing power and low memory environments. Unlike the JVM, the Dalvik Virtual Machine does not run .class files, instead it runs .dex files. .dex files are built from .class file at the time of compilation and provides higher efficiency in low resource environments. The Dalvik VM allows multiple instance of virtual machine to be created simultaneously providing security, isolation, memory management and threading support. It is developed by Dan Bornstein of Google.
+   
+   b. **Core java libraries:** These are different from Java SE and Java ME libraries. However, these libraries provide most of the functionalities defined in the Java SE libraries.

# d. *Application Framework*

These are the blocks that our applications directly interact with. These programs manage the basic functions of phone like resource management, voice call management, etc. As a developer, you just consider these are some basic tools with which we are building our applications.

Important blocks of application framework are:

+   - **Activity Manager:** Manages the activity life cycle of applications.
+   - **Content Providers:** Manage the data sharing between applications.
+   - **Telephony Manager:** Manages all voice calls. We use telephony manager if we want to access voice calls in our application.

# e. *Applications*

Applications are the top layer in the Android architecture and this is where our applications are gonna fit. Several standard applications are pre-installed with every device, such as:

+   - SMS client app
+   - Dialer
+   - Web browser
+   - Contact manager

As a developer we are able to write an application which replace any existing system application. That is, you are not limited in accessing any particular feature. You are practically limitless and can do whatever you want to do with the android (as long as the users of your application permits it). Thus Android is opening endless opportunities to the developer.

# **Applications**

These are the basics of Android applications:

+   - Android applications are composed of one or more application components (activities, services, content providers, and broadcast receivers).
+   - Each component performs a different role in the overall application behavior, and each one can be activated individually (even by other applications).
+   - The manifest file must declare all components in the application and should also declare all application requirements, such as the minimum version of Android required and any hardware configurations required.
+   - Non-code application resources (images, strings, layout files, etc.) should include alternatives for different device configurations (such as different strings for different languages).