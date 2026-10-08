# void EventListenerDispatcher(void *inRefCon,

our self pointer cloaked as a void*,
 we uncloak it and use it to call our own method named

void *inObject,
const AudioUnitEvent *inEvent,
Uint64 inHostTime,
Float32 inValue

```
MiniSynthView* SELF - (MiniSynth*)inRefCon;
[SELF eventListener:inObject
event:inEvent
value:inValue];
```

eventListener:event.value. It seems convoluted but needs to be done like this since the callback is all alone, outside the object definition. Calling the eventListener:value method tells the control to update and redraw itself. Remember that the factory will call setAU method. Look at its implementation:

The AU pointer is named buddyAU and you will use it to call Parameter functions on the AU. After saving it, the View first adds Listeners, then synchronizeUIWithParameterValues, which initializes the GUI with the very first parameter value. Let's look at all of these methods.

-(void)setAU:(AudioUnit)inAU

In addListeners you create the AEventListener as described above, giving your callback function name and a self pointer to store. You need to add a Listener for each of your parameters. This is done in a somewhat convoluted manner:

```
if(buddyAU)
```

```
[self removeListeners];
```

```
// our buddy
```

```
buddyAU = inAU;
```

```
// add new listeners
```

```
[self addListeners];
```

```
// initial setup
```

```
[self synchronizeUIWithParameterValues];
```

+   - create an AUEvent

+   - create an AudioUnitParameter for our first parameter with index 0

+   - set the parameter on the AUEvent

+   - add the event

+   - loop through the rest of the parameters setting the AUEvent's mParameterID variable to the parameter index

+   - add the event