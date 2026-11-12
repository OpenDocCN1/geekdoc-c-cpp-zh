**Step 62:** Tell Unity to listen for the player to press the I button, and if I is pressed, run a function that shows/hides the prompt and the inventory. Do this with a new function Update.

```
```csharp
function Update()
{
    if (Input.GetKeyDown(KeyCode.I))
    {
        ToggleInventory();
    }
}
```
```

# Why?

So the code is saying, "check every frame (function Update) to see if I has been pressed (if (Input.GetKeyDown (KeyCode.I))). If it has, run the function ToggleInventory." Of course, at this point this function doesn't exist ... but it will.

**Step 63:** Write the ToggleInventory function to check if InventoryVisible is true, and if it is, slide the InventoryPrompt on the screen and then slide the buttons off (then lock the cursor and free the camera to look around). If it is not true, have the InventoryPrompt slide off the screen and the buttons on (then unlock the cursor and lock down the camera). Add this function to the bottom of the script:

```
```csharp
function ToggleInventory()
{
    if (InventoryVisible)
    {
        iTween.MoveTo (InventoryPrompt, Vector3 (0, 1, 0), 1);
        iTween.MoveTo (gameObject, Vector3 (-.5, 1, 0), 2);

        InventoryVisible = false;
        Screen.lockCursor = true;
        mainCamera.GetComponent("MouseLook").enabled = true;
        fpcAegis.GetComponent("MouseLook").enabled = true;
    } else {
        iTween.MoveTo (InventoryPrompt, Vector3 (0, 1.1, 0), 1);
        iTween.MoveTo (gameObject, Vector3 (0,1,0), 2);
        InventoryVisible = true;
        Screen.lockCursor = false;
        mainCamera.GetComponent("MouseLook").enabled = false;
        fpcAegis.GetComponent("MouseLook").enabled = false;
    }
}
```
```