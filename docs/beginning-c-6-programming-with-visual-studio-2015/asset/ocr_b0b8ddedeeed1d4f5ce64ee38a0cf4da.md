![](bbox=[0.12, 0.15, 0.93, 0.38])

FIGURE 14-7

# How It Works

By dividing the grid into two columns and two rows, you have changed how the controls can be positioned in the grid. When you set the `Grid.Row` and `Grid.Column` to 0 for the first button, you move it from its previous position on the form to the top-left section.

The second button more or less stays put, but when you drag the `GridSplitter` slider, you see that the margin of the button is now relative to the left edge of the column in which it is placed, meaning that it slides across the window as you move the slider.

# THE GAME CLIENT

Now that you know the basics of what it means to work with WPF and Visual Studio, it is time to start working with the controls to create something useful. The remaining sections of this chapter and Chapter 15 are dedicated to writing a game client for the card game you have been developing over the previous chapters. You are going to use a lot of controls to write the game client, and you are even going to write one yourself.

In this chapter you are going to write the supporting dialog boxes of the game — this includes the About, Options, and New Game windows.

# The About Window

An About window, or About box as it's sometimes called, is used to display information about the developer of the application and the application itself. Some About windows are quite complex, like the one found in Microsoft Office applications and Visual Studio, and display version and licensing