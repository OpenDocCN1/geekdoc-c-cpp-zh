```
System.Windows.Freezable
System.Windows.Media.Animation.Animatable
System.Windows.Media.Animation.Timeline
System.Windows.Media.Animation.TimelineGroup
System.Windows.Media.Animation.ParallelTimeline
System.Windows.Media.Animation.Storyboard
```

The properties of the Storyboard class are same as the Timeline class. The noteworthy property of the Storyboard class which is different from the Timeline class is listed in Table 12.38:

| Table 12.38: Property of the Storyboard Class |
| Property | Description |
| SlipBehavior | Gets or sets a value that specifies how this timeline will behave when one or more of its timeline children slips |

The noteworthy methods of the Storyboard class are listed in Table 12.39:

| Table 12.39: Methods of the Storyboard Class |
| Method | Description |
| Begin | Initiates the set of animations associated with the Storyboard timeline |
| Clone | Creates a modifiable clone of the Storyboard timeline |
| GetCurrentGlobalSpeed | Retrieves the CurrentGlobalSpeed object of the Clock class that was created for the Storyboard timeline |
| GetCurrentIteration | Retrieves the CurrentIteration object of the Clock class that was created for the Storyboard timeline |
| GetCurrentProgress | Retrieves the CurrentProgress object of the Clock class that was created for the Storyboard timeline |
| GetCurrentState | Retrieves the CurrentState object of the Clock class that was created for the Storyboard timeline |
| GetCurrentTime | Retrieves the CurrentTime object of the Clock class that was created for the Storyboard timeline |
| GetIsPaused | Retrieves a value that indicates whether the Clock class that was created for the Storyboard timeline is paused |
| Pause | Pauses the clock that was created for the Storyboard timeline |
| Resume | Resumes the animation clock or runtime-state associated with the Storyboard timeline instance |
| Seek | Seeks the Storyboard timeline to a new position when the next clock tick occurs |
| SeekAlignedToLastTick | Seeks the Storyboard timeline to a new position immediately |
| SetSpeedRatio | Sets the interactive speed ratio for the Clock class that was created for the Storyboard timeline |
| Stop | Halts the Clock class that was created for the Storyboard timeline |

If you are using code to add a Storyboard object to the application, you must create a NameScope for the FrameworkElement object and register the names of the objects to animate with that FrameworkElement. To enable the targeting of the FrameworkElement object in XAML, you set its Name property. In the code-behind file of your application, you need to use the RegisterName() method to register the element name with the element for which you have created a NameScope.

You can interactively control a Storyboard timeline after it has started. Table 12.40 lists a list of Storyboard actions that you use with event triggers to control a Storyboard timeline: