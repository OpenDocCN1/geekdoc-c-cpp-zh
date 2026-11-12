```
```
if (empActive){
    if (!empGhostActive){
        placingEMP = Instantiate(empGhost, hit.point,
hitDir);
        empGhostActive = true;
    }
    if (placingEMP != null){
        placingEMP.transform.position = hit.point;
        placingEMP.transform.rotation = hitDir;
    }
    if (Input.GetMouseButtonDown(0)){
        Destroy (placingEMP);
        placedEMP = Instantiate(empReal, hit.point,
hitDir);
        ExplodeEMP(placedEMP);
    }
}
if (!empActive){
    if (placingEMP != null){
        Destroy (placingEMP);
        empGhostActive = false;
    }
}
```
```

# **Why?**

We want to make sure that if the player uses the EMP tool, but doesn't actually place the EMP, that the ghost version gets deleted. This is especially important later when there are multiple tools that the character can use. So the code says, "If empActive is NOT true, and placingEMP is not empty (as in there is one in the scene), destroy the placingEMP object, and set empGhostActive to false."

**Step 16:** Create the ExplodeEMP to fire the Detonator script. This is another function and so should happen further on down the script (Figure 15.26). Enter the following:

```
```
function ExplodeEMP(placedEMP:GameObject){
    yield WaitForSeconds (2);
    placedEMP.audio.enabled = true;
    placedEMP.GetComponent("Detonator").enabled = true;
    placedEMP.renderer.material.color = Color (0,0,0);
}
```
```

# **Why?**

The first line defines the name of the function and that it can include the parameter of a variable that is a GameObject. Then, when the function is fired, it immediately waits 2 seconds before activating the audio component on placedEMP (placedEMP.audio.enabled = true;) and enabling the script called Detonator on that script (placedEMP.GetComponent("Detonator").enabled = true;), and then changes the color of the material to black (placedEMP.renderer.material.color = Color (0,0,0);).