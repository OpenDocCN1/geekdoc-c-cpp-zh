**FIGURE 5.7** Imported and placed First Person Controller and EntryWay (your results may be a bit different). Not quite right yet, eh?

![](bbox=[0.325, 0.101, 0.935, 0.35])

# ### Why?

When there is little in the scene, moving prefabs into the scene can be a strange experience. It is very tough to understand where an object is in world space or even how big the object is within that space. By moving both the First Person Controller and EntryWay to world center, we can get a good view of what the size is of the imported elements.

**Step 8:** Scale EntryWay to fit appropriately in the scene. To do this, tweak the EntryWay prefab's import settings. In the Project panel, click once on EntryWay. This will open the EntryWay's characteristics in the Inspector. Specifically, in the FBXImporter section, the Inspector will show the settings Unity used when importing EntryWay.fbx into the Unity project. Change the Scale Factor to .5 and press the Apply button. Now adjust the Scale Factor as needed (Figure 5.8).

**FIGURE 5.8** Scaled EntryWay. For this example the setting of 0.5 was the best. This may be different in your scene.

![](bbox=[0.325, 0.627, 0.935, 0.845])

# ### Why?

Why not simply scale the object in the Scene view? In many cases, that would be perfectly acceptable, and actually in this case that would work since the EntryWay prefab is likely to be used only once. However, when a prefab is going to be used a lot of times, it is best to adjust the Scale Factor