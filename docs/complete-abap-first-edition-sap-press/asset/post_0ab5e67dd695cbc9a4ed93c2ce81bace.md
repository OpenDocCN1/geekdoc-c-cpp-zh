
```abap
*&
MODULE user_command_0100 INPUT.

ENDMODULE.
```

**Listing 12.1** Starting Screen Processing in Report Program

## Transaction code

A dialog transaction links the program with its initial screen. When the transaction code is called, it starts the screen sequence by calling the flow logic of the initial screen. From the flow logic of the initial screen, other screens can be called. Figure 12.6 shows Transaction VF01, which links the main program and the initial screen of the billing document application. As previously mentioned, transaction codes are created using Transaction SE93.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_517_0.png)

**Figure 12.6** Transaction VF01

## Screen flow logic

The screen flow logic controls the screen flow and consists of different screen events (as discussed in Section 12.1) from which dialog modules are called. You can only call dialog modules from the screen flow logic, and these dialog modules should be maintained in the main program of the screen.

## Dynpro

The screen along with its flow logic is called a *dynpro* (dynamic program). Each dynpro represents a dialog step of the program.

## Dialog step

A *dialog step* starts with the PAI of one screen and ends with the PBO of the next screen. Each dialog step comprises programming logic between two successive screens. Individual dialog steps of a program can be executed by different work processes in the application server, and a program consists of multiple dialog steps.

During a dialog step, the screen remains inactive for input. For example, the screen is shown to the user in the presentation layer. When the user inputs data on the screen and presses `Enter`, this action initiates the dialog step by calling the PAI event of the screen. The user action is processed by the work process in the application server.

While the work process is processing the request, the screen is visible in the presentation layer but can’t take any input (i.e., the screen is inactive). After the work process has completed processing the request, the same screen or another screen is sent back by the work process, completing the dialog step. Once the screen is sent back to presentation layer, the screen becomes active for user input. At this point, the work process is free to take another request from same user or a different user. Figure 12.7 depicts this request-response cycle.

The number of work processes available in the system is often less than the number of users logged on to the system. Because a work process isn’t dedicated to one user or program, many users can use the system simultaneously. The dispatcher is responsible for distributing all dialog steps among the available work processes in the application server.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_518_0.png)

**Figure 12.7** Request-Response Cycle

Now that we’ve looked at the different components of a dialog program, in the next section let’s hone in on the use of screen components and how to create these screens.

## 12.2.2 Screens

A screen is a repository object that belongs to a program. Screens are dynamic programs (dynpros) that contain their own data objects. The data objects of the screen are called *screen fields* and are linked to the I/O fields on the screen (see Section 12.4 for more on I/O fields). The system passes the data between the screen fields and identically named data objects of the program. This allows us to transfer data from the program to the screen or from the screen to the program.

The screen can be defined for executable programs, module pool programs, and function pools. The process of creating a screen is similar irrespective of the program type. In this chapter, we'll work with module pool programs.

Because a screen is a component of a program, we first need to create a program and then create a screen for a program. We'll use Object Navigator for the examples in this chapter, because it's helpful to work with all the objects in one place.

The following steps illustrate how to create a screen for a program:

1. Open the program in Object Navigator. Right-click the program name and select CREATE • SCREEN, as shown in Figure 12.8.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_519_0.png)

**Figure 12.8** Create Screen Menu Path

2. On the Create Screen dialog box that appears (see *Figure 12.9*), enter the Screen Number and click the green checkmark. The screen number should be unique for the program and can be up to four digits. Screen numbers above 9000 are reserved for SAP customers. The initial screen of the program usually ends with 100.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_520_0.png)

**Figure 12.9** Create Screen Window

3. The system will display the Change Screen Attributes screen (see *Figure 12.10*). This screen consists of three tabs: Attributes, Element list, and Flow Logic.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_520_1.png)

**Figure 12.10** Change Screen Attributes

4. In the ATTRIBUTES tab, various screen attributes can be maintained:

### SCREEN TYPE

In this section, you define the type of screen you want to create. For the screen type, the SELECTION SCREEN option is grayed out, because selection screens aren't defined in Screen Painter but rather are generated using PARAMETERS or SELECT-OPTIONS statements in an ABAP program. This option is automatically selected for the generated selection screen. You can choose one of the following options:

- **NORMAL:** Defines a normal screen. This is the default option and is the type of the main screen. A normal screen acts as a main screen that can have a GUI status and can be called independently in the program or via a transaction code.
- **SUBSCREEN:** This option defines the screen as a subscreen. A subscreen can't be called individually; it's always loaded on the main screen.
- **MODAL DIALOG BOX:** This type of screen is used to display a pop-up screen.

### SETTINGS

Under this section, various settings can be maintained for the screen:

- **HOLD DATA:** If this option is selected, the screen fields will hold data if the user has enabled it under SYSTEM • USER PROFILE • HOLD DATA. This holds any entries made on the screen and will redisplay the data when the screen is processed.
- **SWITCH OFF RUNTIME COMPRESSION:** If this setting is enabled, the screen isn't compressed during runtime. That is, if compression is enabled, the system will automatically remove any lines in which fields were made invisible dynamically. If compression is turned off, then it will show empty lines in such scenarios.
- **TEMPLATE—NON-EXECUTABLE:** This setting is used by SAP internally. This is selected if the screen is to be used as a template for other screens and never executed.
- **HOLD SCROLL POSITION:** Enabling this setting will make the screen hold the scroll position. This is especially useful for large screens. When you come back to the screen after processing another screen, the system will hold the last scroll position.
- Without Application Toolbar: Enabling this setting will hide the application toolbar on the screen.

### Other Attributes

Under the Other Attributes section, the following options can be set:

- Next Screen: You can input the next screen that should be called after PAI of the current screen. This setting can be overridden by using the SET SCREEN statement in one of the PAI modules of the current screen. If the same screen number is entered as the next screen, then the system will call the same screen PBO event after the PAI event and display the same screen.
- Cursor Position: Input the screen field where the cursor should be initially placed when the screen is called.
- Screen Group: Several screens can be assigned to a screen group to perform any modifications consistently on all screens of the group. The screen group name can be accessed by using the SY-DNGR system field.
- Lines/Columns: This setting shows the screen size occupied by the screen elements. This information is useful when calling the screen as a modal dialog box.
- Context Menu Form on CTMENU: You can assign a context menu for the screen in this field.

5. In the Element list tab, all the screen elements that can be maintained will be listed. Figure 12.11 shows the Element list tab with all the screen elements belonging to the screen listed. The screen element details are automatically populated in the Element list tab when we create the screen elements using the layout editor. We'll discuss this tab further when we create screen elements in the next section.

6. The Flow logic tab (see Figure 12.12) allows you to maintain the screen flow logic. The screen events are maintained in the flow logic and are then called by the screen processor. Dialog modules can be called from the flow logic using the MODULE statement.
