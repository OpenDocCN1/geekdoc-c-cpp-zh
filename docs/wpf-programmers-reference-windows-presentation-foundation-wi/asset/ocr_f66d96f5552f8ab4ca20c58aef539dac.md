```
</StringAnimationUsingKeyFrames>

<!-- Display the attribution -->
<DoubleAnimation BeginTime="0:0:2" Duration="0:0:1" To="1">
Storyboard.TargetName="lblBy"
Storyboard.TargetProperty="Opacity"/>
</Storyboard>
```

AnimatedText

The DiscreteKeyFrame class is easy to use, although it's rather tedious you would need to
specify every change to the String individually.

# CONTROLLING STORYBOARDS

In addition to the BeginStoryboard class, which starts a Storyboard running, WPF provides sev-
eral objects for controlling Storyboards. The most useful of these classes are:

+   - PauseStoryboard — Pauses a Storyboard.
- ResumeStoryboard — Resumes a paused Storyboard.
- SeekStoryboard — Moves the Storyboard to a specific position in its timeline.
- StopStoryboard — Stops a Storyboard. This resets properties to their original values.
- RemoveStoryboard — Stops a Storyboard and frees its resources.

Many of the examples in this chapter demonstrate most of these classes. For example,
the RunningButtonMixedKeyFrames example program in Figure 14-9 provides Start, Pause,
Resume, Stop, and Remove buttons to control your Storyboard.

The following code shows how these examples manage their Buttons:

```
<EventTrigger RoutedEvent="Button.Click" SourceName="btnStart">
<EventTrigger.Actions>
<BeginStoryboard Name="begSbButton"
="StaticResource sbMoveButton"/>
<EventTrigger.Actions>
</EventTrigger>
```

```
<EventTrigger RoutedEvent="Button.Click" SourceName="btnPause">
<EventTrigger.Actions>
<PauseStoryboard BeginStoryboardName="begSbMoveButton"/>
<EventTrigger.Actions>
</EventTrigger>
```

```
<EventTrigger RoutedEvent="Button.Click" SourceName="btnResume">
<EventTrigger.Actions>
<ResumeStoryboard BeginStoryboardName="begSbMoveButton"/>
<EventTrigger.Actions>
</EventTrigger>
```

```
<EventTrigger RoutedEvent="Button.Click" SourceName="btnStop">
```

![](bbox=[0.085, 0.623, 0.158, 0.673])

Available for
download on
W3x.com