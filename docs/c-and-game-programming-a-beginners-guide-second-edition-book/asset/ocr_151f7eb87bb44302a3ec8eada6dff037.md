| Methods, Properties: | Description: |
|---|---|
| BufferPlayFlags.Default | Default, the first property of the method public enum BufferPlayFlags allocates to hardware and software. |
| BufferPlayFlags.LocateInHardware | Boolean type; sound supported through hardware. |
| BufferPlayFlags.LocateInSoftware | Boolean type; sound supported through software. |
| BufferPlayFlags.Looping | Looping. Repeats sound indefinitely. |
| BufferPlayFlags.TerminatebyDistance | Selects buffer by 3D distance (farthest). |
| BufferPlayFlags.TerminatebyPriority | Selects buffers by priority (lowest priority). |
| BufferPlayFlags.TerminatebyTime | Selects buffer by time (longest running). |

**Table 3.0. Sound Methods and Properties.**

# ## Adding in the Mouse

Another interesting feature to add to our games is the little object sitting to the side of our keyboards (yes, I mean the mouse). The mouse was invented in the 1960s by a man named Douglas C. Engelbart of Stanford Research Institute (SRI), and later put to use at the Xerox Palo Alto Research Center (known as PARC) as part of the first Graphical User Interface (or GUI). The mouse was also made popular by Steven Jobs with the release of a primitive type of computer known historically as the Macintosh... The basic controls we want to work with include the OnMouseUp, OnMouseDown, OnMouseMove, and the OnMouseWheel (Note: the OnMouseWheel also requires an IntelliMouse, a specially designed three button mouse manufactured by Microsoft). The two key functions we'll work with are OnMouseMove and OnMouseDown events, but the other two can be applied in basically the same manner.

Note: We'll also want to use the x, y coordinates to mark the graphical positioning. The constant 341 is used to restrict a character's movements horizontally; no vertical restrictions are required, since they would not affect the limitation implied by the rules of the game. One should also note that these movements would not be updated unless the ball is also found to be in motion; this is done to reduce screen static, or flickering that is caused by excessive updates (see Example 3.29).