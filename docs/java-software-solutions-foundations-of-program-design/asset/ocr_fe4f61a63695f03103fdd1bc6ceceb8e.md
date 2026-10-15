c. The rocket ship and flames now appear sideways (i.e., horizontal), because exchanging the x and y coordinates of all of the points reflects the drawing across the line x = y.

d. The rocket ship and flames are framed by a yellow diamond; because the yellow polygon is drawn first, everything else is visible on top of it.

e. Almost all of the picture is hidden by the yellow polygon; because the yellow polygon is drawn last, it hides the other components of the drawing that fall within its coordinates.

# 8.8 Mouse Events

SR 8.28 A mouse event is an event generated when the user manipulates the mouse in various ways. There are several types of mouse events that may be of interest in a particular situation, including the mouse being moved, a mouse button being pressed, the mouse entering a particular component, and the mouse being dragged.

SR 8.29 The sequence of events is mouse pressed, mouse released, and mouse clicked.

SR 8.30 The sequence of events is mouse pressed, mouse exited, and mouse clicked. There are also a series of mouse motion events generated.

SR 8.31 The mouse event responded to in the Dots program is mouse pressed. The mouse events responded to in the RubberLines program are mouse pressed and mouse dragged.

SR 8.32 Some possible responses are: highlight a game square when a mouse enters its space, if it represents a legal move; place an X (or an O) in a game square if the user clicks on it at the appropriate time; allow the user to drag an X (or an O) to a square.

# 8.9 Key Events

SR 8.33 A key event is generated when a keyboard key is pressed, which allows a listening program to respond immediately to the user input. The object representing the event holds a code that specifies which key was pressed.

+   SR 8.34
+    a. keyPressed
+    b. keyTyped, keyReleased
+    c. VK_UP
+    d. arrowLeft.gif
+    e. arrowRight.gif