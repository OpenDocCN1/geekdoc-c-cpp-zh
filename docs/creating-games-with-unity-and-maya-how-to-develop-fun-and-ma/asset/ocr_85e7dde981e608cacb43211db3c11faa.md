![](bbox=[0.0, 0.09, 1.0, 0.44])

# # Unity: Creating Inventory Systems

Thus far we have created several weapons and tools (our flashlight, EMP, and pistol). However right now, in order to use any of the three, they have to be activated in the script manually before running the game. This, of course, is a useless method to the player. What we need to do is create an inventory system that allows the player to choose which tool he wants to use and when. This inventory system will also do the work behind the scenes of turning various tool functionality on and off in the scripts.

Right now, the gun is active even when placing an EMP. The flashlight is shining even when the flashlight isn't visible. We need to get these tools so we use them one at a time. Before we get to the nitty-gritty, though, there are a few core ideas to cover.

# ## State Engine and How Many Scripts?

A state engine is a mechanism that (for our purposes) will keep track of what state the game is in. Or more directly, what state the player is in. Or more specifically, what weapon/tool the character is using. It turns out we've actually been creating one as we've been building the AC_ToolFunctionalityScript.