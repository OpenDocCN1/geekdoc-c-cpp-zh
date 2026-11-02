# WHAT YOU HAVE LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Detect touches on the view | Handle the following event in the view or View Controller:
* `touchesBegan:withEvent:`
* `touchesEnded:withEvent:`
* `touchesMoved:withEvent:`
* `touchesCancelled:withEvent:` |
| Detect for taps (single, double, and so on) | You can detect for taps either in the `touchesBegan:withEvent:` or `touchesEnded:withEvent:` methods. |
| Implement "pinch" gesture | Compare the distance made by the two touch points and deduce whether the gesture is zoom in or out. |
| Implement "drag" gesture | Ensure that the touch point falls within the area occupied by the view in question. |