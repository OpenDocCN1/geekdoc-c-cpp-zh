In Figure 12.3, all four screen events listed are maintained with their respective event statements. Dialog modules are called from the event block using the MODULE statement. The dialog modules that are called from the screen flow logic should be maintained between the MODULE...ENDMODULE statements in the main program to which the screen belongs (refer ahead Figure 12.5).

![](bbox=[0.1476, 0.2222, 0.5745, 0.4133])

**Figure 12.3** Screen Flow Logic

The PBO event is triggered before the screen is shown to the user, and the remaining events are triggered after the screen is shown. The PBO event allows you to prepare the screen before it’s displayed to the user, and other events allow you to react to user actions on the screen. For example, if you want to disable a field on the screen or hide some of the screen elements dynamically, you can use the PBO event.

Similarly, you can capture user inputs and process the application in the PAI event. The POH and POV events allow us to extend an application's functionality by providing additional help for the screen fields. This helps the user understand what input is expected in each screen field or search for a valid input. The field help documentation along with input helps provides a consistent user experience for the user throughout the SAP system.

# 12.2 Screen Elements and Flow Logic

When we develop dialog programs, we work with ABAP Workbench tools to create different objects. For example, we use Screen Painter (Transaction SE51) to create and design a screen, and we use Menu Painter (Transaction SE41) to define the GUI status for the screen.