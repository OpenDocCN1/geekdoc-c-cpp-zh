Of course, Java development environments have drag-and-drop GUI builders. Nevertheless, it is important to know exactly what goes on “under the hood” because even the best of these tools will usually require hand-tweaking.

# 11.2.1 Layout Managers

Let’s start by reviewing the program from Listing 10.4 that used buttons to change the background color of a frame.

The buttons are contained in a JPanel object and are managed by the *flow layout manager*, the default layout manager for a panel. Figure 11.4 shows what happens when you add more buttons to the panel. As you can see, a new row is started when there is no more room.

![](bbox=[0.267, 0.383, 0.646, 0.578])

**Figure 11.4** A panel with six buttons managed by a flow layout

Moreover, the buttons stay centered in the panel, even when the user resizes the frame (see Figure 11.5).

![](bbox=[0.321, 0.69, 0.591, 0.886])

**Figure 11.5** Changing the panel size rearranges the buttons automatically.