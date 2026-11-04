Many of these apps also don't provide buttons or menu items that let the user close them. Instead the user simply opens or navigates to another app and leaves yours sitting in the background. Later the device closes your app if it needs to free up memory.

> > **NOTE** Although many apps don't provide a way to close them, you can close an app by making the code call `Application.Current.Exit()`.

Because these apps cover the entire device, you must arrange the controls to take best advantage of whatever space is available. You don't have control over how large the user's screen is, so you should use container controls such as Grid and StackPanel to get the most out of the space you have.

# ## APP STYLES

Visual Studio includes templates for building several different styles of Windows Store apps. The following list summarizes the most common kinds of Windows Store templates:

+   - **Blank**—This kind of app displays a single window with no navigation to other windows. It's similar to a one-window desktop application without dialogs.
+   - **Hub**—This kind of app uses a Hub control. The main Hub control displays a horizontally scrolling window divided into sections holding different kinds of information. You can tap a section heading to open a new page that provides details about that section.
+   - **Grid**—This kind of app displays sections in a grid. You can tap a section to open a list of items in that section. If you then tap an item in the list, the app opens a full page about that item.
+   - **Split**—This kind of app displays a list and a detail area. You can tap an item in the list to see its details.
+   - **Pivot**—This kind of app displays a collection of list categories. When a category is selected, you see its list of items below it. You can scroll horizontally through the different categories. This template is useful for displaying different views of data. For example, my phone displays Outlook mail in a pivot view with categories All, Unread, and Urgent.

If you use one of these templates to create a new project, the app comes pre-loaded with sample data so you can see what the finished app will look like. (In fact, you'll probably get a better sense of how the different templates work if you just create some sample projects and run them rather than starting at the previous descriptions.)

# ## APP IMAGES

Windows and the Windows Store can represent your app in many ways using images with different sizes. For example, the Windows Start screen can displays your app's tile in Small, Medium, Wide, and Large sizes.