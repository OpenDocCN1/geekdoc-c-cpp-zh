the exact place it was before. (An app receives a flag on startup to indicate its previous execution state, which determines what it should do with saved session state. Details are in Chapter 3.)

There's another dimension to statefulness: remember from earlier in this chapter that a user can install the same Windows Store app on up to five different devices? Well, that means that an app, depending on its design, of course, can also be stateful between those devices. That is, if a user pauses a video or a game on one device or has made annotations to a book or magazine on one device, the user will naturally want to be able to go to another device and pick up at exactly the same place.

Fortunately, Windows makes this easy—really easy, in fact—by automatically roaming app settings and state, along with Windows settings, between trusted devices on which the user is logged in with the same Microsoft account, as shown in Figure 1-10.

![](bbox=[0.14, 0.32, 0.86, 0.6])

FIGURE 1-10 Automatic roaming of app roaming data (folder contents and settings) between devices.

The key here is understanding how and where an app saves its state. (We already know when.) If you recall, there's one place on the file system where an app has an unrestricted access: its appdata folder. Within that folder, Windows automatically creates subfolders named LocalState, RoamingState, and TempState when the app is installed (I typically refer to them without the "State" suffix.) The app can programmatically get to any of these folders at any time and can create in them all the files and subfolders to fulfill its heart's desire. There are also APIs for managing individual Local and Roaming settings (key-value pairs), along with groups of settings called composites that are always written to, read from, and roamed as a unit. (These are useful when implementing the app's Settings features for the Settings charm, as covered in Chapter 10, "The Story of State, Part 1.")

Now, although the app can write as much as it wants to the appdata areas (up to the capacity of the