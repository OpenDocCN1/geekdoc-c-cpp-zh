ProcessInput function. This way, actors can query the input state for not only the current values of inputs but also negative and positive edges.

For devices that give a range of values, such as the triggers or analog sticks, you typically need to filter this data. This is because even when the device is at rest, the device may give spurious signals. The filtering implemented in this chapter ensures that input less than some dead zone is ignored and also ensures that you detect the maximum input even when the input is only “almost” the maximum.

This chapter’s game project takes advantage of the new controller input functionality to add support for twin-stick shooter–style movement.

# ADDITIONAL READING

Bruce Dawson covers how to record input and then play it back, which is very useful for testing. The Oculus SDK documentation covers how to interface with Oculus VR touch controllers. Finally, Mick West explores how to measure input lag, which is the amount of time it takes a game to detect inputs from controllers. Input lag is generally not the fault of the input code, but West’s material is interesting nonetheless.

Dawson, Bruce. “Game Input Recording and Playback.” Game Programming Gems 2, edited by Mark DeLoura. Cengage