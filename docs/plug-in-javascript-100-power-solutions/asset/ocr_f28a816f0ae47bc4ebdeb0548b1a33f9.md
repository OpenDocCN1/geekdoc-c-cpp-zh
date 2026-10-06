# Chapter 7: Chaining and Interaction 179

| Chain() | DeflateToggle() | FadeToggle() | Repeat() | While() |
|---|---|---|---|--|
| CallBack() | Fade() | Hide() | Show() | Zoom() |
| ChainThis() | FadeBetween() | HideToggle() | Slide() | ZoomDown() |
| Deflate() | FadeIn() | Pause() | SlideBetween() | ZoomRestore() |
| DeflateBetween() | FadeOut() | Reflate() | WaitKey() | ZoomToggle() |

**Table 7-1** The Plugins that Support Chaining can be called by plugging-in via a callback. 

Table 7-2 lists the plug-ins that not include any other plug-in within a chain sequence (unless you use the ChainThis() plug-in, discovered later), they will not call any remaining plug-ins in a chain, so a sequence may be interrupted. However, you can always include your own plug-ins in a chain if you place a call to NextChain() after the first instruction has executed.

> > Never attempt to insert any of the Chain(), Repeat(), or While() plug-ins into a chain or you'll get "out of memory," recursion, and possibly other errors. These functions can be only used for creating chains that do not contain calls to themselves.

The NextChain() and CallBack() plug-ins are generally not expected to be called directly, although you can do so using the information that follows.

# Variables, Arrays, and Functions

| j | Local variable to iterate through the calls array |
|---|--|
| CHAIN_CALLS | Global array in which chained plug-ins are stored prior to their execution. |
| push() | Function to push a value onto an array |
| pop() | Function to pop a value off an array |
| eval() | Function to evaluate a string as JavaScript code |

# How They Work

The ChainThis() plug-in takes the stored in the calls array and pushes them all onto the global CHAIN_CALLS array. Because the last item pushed onto an array is always the

| ChainThis() | FadeIn() | Reflate() | ZoomDown() |
|---|---|---|---|--|
| Deflate() | FadeOut() | Show() | ZoomRestore() |
| DeflateBetween() | FadeToggle() | Slide() | ZoomToggle() |
| DeflateToggle() | Hide() | SlideBetween() | |
| Fade() | HideToggle() | WaitKey() | |
| FadeBetween() | Pause() | Zoom() |

**Table 7-2** The Plugins That Support Being Chained or Using Callbacks