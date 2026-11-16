# # TRIGGER ACTIONS

The Actions collection of the EventTrigger accepts members of the abstract TriggerAction class. You can create your own actions by deriving from TriggerAction, but you'll most often work with one of the three trigger action classes defined in the Framework Library.

![](bbox=[0.18, 0.24, 0.88, 0.6])

The ControllableStoryboardAction is also abstract. The classes that derive from it let you start, stop and pause storyboard animations.

The BeginStoryboard action plays an animation. We'll be looking at animations in a few pages.

The SoundPlayerAction does exactly what you'd expect: It plays a sound.

# ## PUT ON YOUR THINKING HAT ...

We'll be looking at the BeginStoryboard trigger action and simple storyboard animations in a bit, but to get a sense of how event triggers work (it's easy), delete those duplicate definitions we added to FluentDictionary in the last exercise and then replace the IsMouseOver property trigger of the Button style with a Click event trigger.

You can set the Source property to any .wav file. (Search for '*.wav' in the Windows Explorer to find one, and then add it to your project.)