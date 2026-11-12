```
if (name == "Button-PlayAgain"){
	Application.LoadLevel("Scene-Opening");
}
```

**Step 7:** Save and return to Unity. Fix syntax problems.

**Step 8:** Apply CloseScreenButtonScript to Button-Exit and Button-PlayAgain in the Hierarchy.

**Step 9:** Change the color value of Button-Exit and Button-PlayAgain to RGB=50. Remember to do this, select each button in the Hierarchy; then in the GUITexture component, click the color swatch to change the values.

**Step 10:** Play and test. When the Exit button is clicked nothing will happen (it'll work when the game is built though). When the Play Again button is clicked, we should be back in Scene-Opening.

**Step 11:** Save Scene-Closing.

# ## The Endgame Trigger

**Step 12:** Open Scene-Hallway.

**Step 13:** Create a trigger that sits right in front of the closet where the device resides (at the bottom of the stairs (Figure 17.3)). Name it Trigger-Endgame.

![](bbox=[0.37, 0.52, 0.88, 0.79])

> **Tips and Tricks**
> 
> Note that Figure 17.3 shows the positioning of the trigger with Unbaked hidden, and Baked visible (although it could also be placed by disabling the lighting in the Scene view).