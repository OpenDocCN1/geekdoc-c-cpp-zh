
While there is no substitute for getting your hands on a real device, the following bada design points are worth bearing in mind:

- Touch – finger-based direct manipulation including multi-touch, pinching and swiping, and of course tactile feedback.
- Simplicity – simple screen layout, relatively large and bold fonts, large GUI elements for interaction, large simple icons, limited customisation, simple menus.
- Bright and bold – making the most of superAMOLED display technology, high contrast, vivid colours, saturated blacks (and by the way, dark colour schemes are preferred to light, because with AMOLED technology dark pixels consume less power than light pixels).
- Extended user input – as well as touch and hard keys, the touch UI supports gestures (physical motions including tapping on the case, rotating the phone, snap and shake), and even face detection.
- Multiple display sizes and resolutions – WVGA (Wide VGA) 480 × 800, WQVGA (Wide Quarter VGA) 240 × 400.

You can find detailed UI guidelines in the SDK Help. Select Help | Help Contents | bada Application UI Guide in the IDE.

### 2.2.1 Frames, Forms, and Controls

The GUI is not just what you see on the screen. The simplicity of bada’s touch UI look-and-feel extends to the architecture beneath it, and to the concepts that motivate the architecture. While bada won’t design your GUI for you, it does provide a simple and standardised GUI architecture for your app to use.

You can think of everything your app displays as being organised in a hierarchical tree. The root of the tree is the application Frame. Within every app, the Frame is the top-level container to which all GUI elements are added. More formally, the Frame class encapsulates the device display, and plays the role of the application’s top-level window, of which there is exactly one per application. All applications have a Frame, and you don’t need to do anything to create it or set it up. It’s all taken care of by the framework.

Standard controls that are ready-made by the framework, or your own derived custom controls. The Control class abstracts a screen region, both for display and capturing input.

Naturally, bada provides comprehensive graphical primitives, bitmaps, animations, and fonts, so the real limits here are your imagination – and your design skills!⁴ The relationship between Frames, Forms, and Controls is shown in Figure 2.8.

> ⁴Under the hood, the raw horsepower for bada’s graphics capabilities is based on OpenGL ES, with support for 2.0 (hardware acceleration and hardware shaders) and 1.1 standards (hardware acceleration only). The OpenGL ES version available is device dependent. It is also possible that at the low end, some bada phones will not support OpenGL ES at all. Apps that require OpenGL ES will not install on phones that lack appropriate support.

![](img/a257d5fd53a79a244a20e587cd2f08f6_54_0.png)

Figure 2.8 All applications have a Frame, the top level container within which Forms are added; Forms are populated with Controls.

### 2.2.2 Standard Elements of a Form – Indicator Bar, Title Bar, Soft Keys, Option Menu

A Form occupies the full physical display area of the phone – everything visible on the screen. Forms therefore also optionally include some standard system elements (see Figure 2.9). These are

- The Indicator bar at the top of the display area, used to display system icons (such as signal and battery strength) and notifications (such as whether you have unread messages).
- The Title bar, which can display a string.
- Soft keys that are displayed in the command area at the bottom of the main display.
- The Option menu key, displayed at the bottom of the display area between the soft keys, used to launch an Option menu.

The system elements are defined as properties of the Form. The decision whether to display all or some of them is made by each Form, and is therefore under the control of the application that defines the Form. However, their look and feel (and in the case of the Indicator bar, its contents too) is not directly controlled by the app. Although the Form displays the system elements, the framework retains control of them.

![](img/a257d5fd53a79a244a20e587cd2f08f6_55_0.png)

**Figure 2.9** The application name and standard system elements.

### 2.2.3 Handling Events

We said that every Control-derived class abstracts a screen region, both for display and input, but we didn’t say how. Input events include input from the touch screen, including menus and soft keys, from the physical phone keys including side keys such as Lock and Camera, from gestures and raw sensor events, from bada system events – potentially from *any* type of event.

Listeners are the glue that binds behaviour to presentation in a bada app. In bada, listeners provide the mechanism for all event handling. At any time, exactly one control has *focus* in the GUI. *Focus* just means which object is actively updating the display and receiving user and system events. Conceptually, focus belongs to the currently active control of the currently running foreground application. This control receives any input events that occur (and by the way, also initiates redrawing the display).

Every control has built-in listeners for the basic event types it recognises. Depending on the control, these might include any of the following:

- Focus events
- Key events
- Touch events
- Drag and drop events

## The BuddyFix UI

BuddyFix is a simple app that enables a simple use-case. It enables a user to share periodically updated location information with a list of friends in order to converge in real-time on a meeting place. To do so, BuddyFix uses the Buddy service that bada provides as a service API.

BuddyFix displays a list of buddies, with the following information displayed for each buddy:

- picture;
- name;
- location fix, i.e. last known location;
- time fix, i.e. time of last location fix;
- location status, on or off the grid, i.e. currently reachable or not;
- whether location sharing is enabled for this buddy.

Additionally the UI must provide the following information:

- whether sharing is paused or active at application level;
- interval at which location fixes are updated.

Points to note:

- Location sharing is always in both directions.
- Location fixes are therefore always updated in both directions.
- Application-level pausing of location sharing allows power to be saved.
- Location display format should be user selectable.
- Location sharing is periodic not continuous, and is scheduled according to the update interval.
- The update interval should be user selectable.
- The update interval applies to all buddies.
- Individual buddies are added from the phone Contacts app.
- Friends must already be buddies on the Buddy service to be allowed by BuddyFix.

Clearly, some of the above are too limiting for the app to be fully featured, but for current purposes they keep complexity manageable.

The UI must enable the following actions:

- Add/Remove a buddy.
- Start/Stop sharing, for some buddy.
- Nudge now, share a location fix with some buddy now, without waiting for the next scheduled update.
- Set the update interval.
- Pause/Unpause all sharing.

So let's get started. We'll define a single MainListForm as the basic app screen, from which all functionality will be available. Launch the Resource Explorer by selecting Window | Show View | Other from the Eclipse main menu bar as shown in Figure 2.10.

![](img/a257d5fd53a79a244a20e587cd2f08f6_58_0.png)

Figure 2.10 Launching the Resource Explorer.

The Resource Explorer pane will open in the IDE. (If it is empty when it launches, make sure you have your project selected in the Project Explorer pane.) Right-click anywhere in the Resource Explorer and select Open Insert Wizard, as shown in Figure 2.11. It's a new Form we want to create, so select Create Form File, and Finish. A new Form appears in the Resource Explorer pane. Double click to launch the WYSIWYG UI Builder and you should see the screen shown in Figure 2.12. Note that the default Form – for demonstration purposes – already contains a Button control, which you can use or simply delete. When the UI Builder pane is launched, double-click on the main Form pane to open the Form Properties pane as shown in Figure 2.13.

### 2.3.2 Form Properties

Before doing anything else, let's change the Form name to something meaningful. Properties are simple name, value pairs. To edit a property, double click the property name in the property list and change the associated value. For BuddyFix, we retain the 'IDF' prefix and the all-caps resource naming convention to provide clarity in our code, and name the Form IDF_MAIN_LIST_FORM.
