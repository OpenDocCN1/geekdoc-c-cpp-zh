Nowadays, one would implement do-nothing methods of the windowListener interface as default methods. However, Swing was invented many years before there were default methods.

# ### java.awt.event.WindowListener 1.1

+   - `void windowOpened(WindowEvent e)`
+     is called after the window has been opened.
+   - `void windowClosing(WindowEvent e)`
+     is called when the user has issued a window manager command to close the window. Note that the window will close only if its `hide` or `dispose` method is called.
+   - `void windowClosed(WindowEvent e)`
+     is called after the window has closed.
+   - `void windowIconified(WindowEvent e)`
+     is called after the window has been iconified.
+   - `void windowDeiconified(WindowEvent e)`
+     is called after the window has been deiconified.
+   - `void windowActivated(WindowEvent e)`
+     is called after the window has become active. Only a frame or dialog can be active. Typically, the window manager decorates the active window—for example, by highlighting the title bar.
+   - `void windowDeactivated(WindowEvent e)`
+     is called after the window has become deactivated.

# ### java.awt.event.WindowStateListener 1.4

+   - `void windowStateChanged(WindowEvent event)`