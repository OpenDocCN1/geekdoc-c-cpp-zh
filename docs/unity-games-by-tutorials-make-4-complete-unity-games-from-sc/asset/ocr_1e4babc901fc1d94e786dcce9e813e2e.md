Finally, the last line of code checks that the scene is set to Menu before calling DiscoverLevels(). This check ensures the script did indeed discovers all of the level files and how many different buttons are ready to load the associated level paths.

Save GameManager.cs and run the game from the Menu scene.

Choose one of those custom-designed levels saved to JSON from the Menu level selector.

![](bbox=[0.119, 0.247, 0.87, 0.417])

The level is loaded from the file and completely re-constructed.

Congratulations! You now have a fully functional level loader, with the ability to design and save custom levels, as well as display them in the menu's level selector scrolling panel.

# Tidying up loose ends

There are a few things to tidy up. Remember those best times you implemented with binary serialization? Well, they only work on one level.

No matter how many levels you create and play, the same times show up for all of them.

Currently, best times to save to a binary file are concatenated with whatever name you choose to play and the suffix times.dat.

| Name | Date modified | Type | Size |
| --- | --- | --- | --- |
| sean_times.dat | 26/08/2016 18:59 | DAT File | 1 KB |

It'll work better if you tie the best times to the level names.