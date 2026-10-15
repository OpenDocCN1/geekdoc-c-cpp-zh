Key events fire whenever a key is pressed, but most systems enable the concept of *key repetition*. That is, when a key is pressed and held down, it’s as if that key is being pressed repeatedly and quickly. Key events are generated in the same way. In the Direction program, the user can hold down an arrow key and watch the image move across the screen quickly.

The component that generates key events is the one that currently has the *keyboard focus*. Usually the keyboard focus is held by the primary “active” component. A component usually gets the keyboard focus when the user clicks on it with the mouse. The call to the `setFocusable` method in the panel constructor sets the keyboard focus to the panel.

The Direction program sets no boundaries for the arrow image, so it can be moved out of the visible window, then moved back in if desired. You could add code to the listener to stop the image when it reaches one of the window boundaries. This modification is left as a programming project.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 8.33 What is a key event?

SR 8.34 Answer the following questions about our Direction program.

+   a. Which key pressed events are responded to?
+   b. Which key pressed events are not responded to?
+   c. What is the key code for the up-arrow key?
+   d. In what file do we store the left-arrow image?
+   e. Which image is displayed when the program begins?