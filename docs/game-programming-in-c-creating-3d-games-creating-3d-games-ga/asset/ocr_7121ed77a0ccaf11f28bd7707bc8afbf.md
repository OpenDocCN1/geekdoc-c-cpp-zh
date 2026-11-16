![](bbox=[0.17, 0.09, 0.72, 0.42])

Figure 8.4 Ship moving around in the Chapter 8 game project

# SUMMARY

Many different input devices are used for games. A device might report either a single Boolean value or a range of inputs. For a key/button that reports a simple on/off state, it’s useful to consider the difference between the value in this frame and the value in the last frame. This way, you can detect the positive or negative edge of the input, corresponding to a “pressed” or “released” state.

SDL provides support for the most common input devices including the keyboard, mouse, and controller. For each of these devices, you add data in an InputState struct that you then pass to each actor’s