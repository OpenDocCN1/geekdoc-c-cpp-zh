The list of songs that is displayed in the combo box is defined in an array of strings. The first entry of the array will appear in the combo box by default and is often used to direct the user. We must take care that the rest of the program does not try to use that option as a valid song.

The play and stop buttons are displayed with both a text label and an image icon. They are also given mnemonics so that the jukebox can be controlled partially from the keyboard.

A combo box generates an action event whenever the user makes a selection from it. The JukeBox program uses one action listener class for the combo box and another for both of the push buttons. They could have been combined, using code to distinguish which component fired the event.

The actionPerformed method of the ComboListener class is executed when a selection is made from the combo box. The current audio selection that is playing, if any, is stopped. The current clip is then updated to reflect the new selection. Note that the audio clip is not immediately played at that point. The way this program is designed, the user must press the play button to hear the new selection.

The actionPerformed method of the ButtonListener class is executed when either of the buttons is pushed. The current audio selection that is playing, if any, is stopped. If it was the stop button that was pressed, the task is complete. If the play button was pressed, the current audio selection is played again from the beginning.

# SELF-REVIEW QUESTIONS *(see answers in Appendix N)*

+   SR 11.23  What is a combo box?
+   
+   SR 11.24  How does the JukeBox program ensure that it doesn’t try to play a song associated with the "Make a Selection . . ." combo box option?
+   
+   SR 11.25  How many action listeners are defined in the JukeBox program, and what do they each listen for?
+   
+   SR 11.26  Describe in detail how the JukeBox program associates the combo box selection made by the user with a specific audio clip.

# 11.9 Scroll Panes

Sometimes we need to deal with images or information that is too large to fit in a reasonable area. A scroll pane is often helpful in these situations. A scroll pane is a container that offers a limited view of a component, and provides vertical or horizontal scroll bars to change that view. At any point, only part of the underlying component can be seen, but the scroll bars allow the user to navigate to any