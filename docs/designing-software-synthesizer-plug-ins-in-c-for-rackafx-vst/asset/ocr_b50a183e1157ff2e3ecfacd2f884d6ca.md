Client. You can use the built-in MIDI piano control (limited) or any Windows compatible MIDI input device (recommended) to generate the MIDI messages needed to test the plug-in.

# Creating and Saving Presets

The presets are created and maintained on the main RackAFX UI. After you load your plug-in you can move the controls like you and then save them as a preset. Use the Save Preset button on the toolbar. The presets will be saved inside a file until the next time you compile your plug-in; after that, the presets will be built into the DLL. You can add, modify, or delete the presets when your plug-in is loaded.

# 2.7 Setting Up RackAFX

Start the RackAFX soft ware. You will start in Prototype View where you will see a blank control surface shown in Figure 2.2. Your GUI may look slightly different or have different background images.

The control surface is what you use to create your user interface. It is full of assignable controls you can connect to your plug-in's variables. The surface consists of:

+   1. 40 assignable sliders (continuous controls)
2. universal LCD control with 1024 more continuous controls inside
3. project controls (open, load, edit, rebuild, debug, jump-to-C++)
4. 4 on-off 2-state switches
5. mini-analyzer with scope and spectrum analyzer and joystick control (for vector synths)
6. assignable buttons
7. 10 assignable LED meters
8. input/output controls
9. prototype tab: the main GUI
10. GUI Designer tab: opens the designer for editing; you must have GUI controls declared first