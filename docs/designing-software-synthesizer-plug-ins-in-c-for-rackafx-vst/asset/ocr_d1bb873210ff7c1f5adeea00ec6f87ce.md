# The

```
(void)addListeners
{
    if (buddyAU)\    {
        // --- create the event listener
        // and tell it the name of our Dispatcher function
        // EventListenerDispatcher
        verify_noerr(AUEventListenerCreate(EventListenerDispatcher, self,
            CFRunLoopGetCurrent(),
            kCFRunLoopDefaultMode, 0.05,
            0.05,
            &EventListener));

        // --- start with first control 0
        AudioUnitEvent aEvent;
        // --- parameter 0
        AudioUnitParameter parameter = (buddyAU, 0,
            kAudioUnitScope_Global, 0);

        // --- set param & add it
        aEvent.mArgument.mParameter = parameter;
        addParamListener(AUEEventListener, self, &aEvent);

        // parameters 1 -> NUMBER_OF_SYNTH_PARAMETERS-1
        // notice the way additional params are added using
        mParameterID
        for (int i=1; i<cNUMBER_OF_SYNTH_PARAMETERS; i++) {
            aEvent.mArgument.mParameter.mParameterID = i;
            addParamListener(AUEEventListener, self, &aEvent);
        }
    }
}
```

removeListener method simply disposes of the EventListener.