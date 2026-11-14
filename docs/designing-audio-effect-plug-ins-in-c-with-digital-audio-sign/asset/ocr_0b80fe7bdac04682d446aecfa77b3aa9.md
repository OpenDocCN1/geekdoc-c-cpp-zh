![](bbox=[0.3, 0.01, 0.7, 0.07])

# Figure 3.4: The volume control block diagram.

> Coefficients in a block diagram (or transfer function or algorithm) become float member variables in your plug-in code.

+   - a_2 = 0: Mute
+   - a_2 = 1.0: Max volume

The output samples y(n) are a scaled version of the input x(n) and the scaling factor is named a_2. a_2 is called a coefficient in the algorithm. The algorithm states that a_2 will vary between 0 (mute) and 1.0 (full volume).

# 3.8 Set up RackAFX for Use

Start the RackAFX software. You will start in prototype view, where you will see a blank control surface as shown in Figure 3.5. Your GUI may look slightly different or have different background images.

The control surface is what you use to create your UI. It is full of assignable controls you can connect to your plug-in's variables. The surface consists of:

+   - 40 assignable sliders (continuous controls).
+   - Universal LCD control with 1024 more continuous controls.
+   - Project controls (open, load, edit, rebuild, debug, jump to C++).
+   - Vector joystick (advanced, see website for more details).
+   - Assignable buttons.
+   - 10 assignable LED meters.
+   - Plug-in routing controls to test insert and aux effect modes.
+   - Prototype tab, the main GUI.
+   - GUI designer tab, which opens the designer for editing; you must have GUI controls declared first. See the website for more details.

The menu and toolbar consist of two parts: the left and right side. The left side (Figure 3.6) implements the majority of the software functionality, while the right side (Figure 3.7) maintains lists.