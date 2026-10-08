2. Display an NSOpenPanel, restricting the user’s choices in that panel to the file types in your array.

In this instance, you aren’t restricting the sound file types because you used soundUnfilteredFileTypes in Step 1, which populates the array with all possible sound file types. Limit the number of files a user can open in the NSOpenPanel to only one file:

```
NSOpenPanel \*theOpenPanel = [NSOpenPanel openPanel];
[theOpenPanel setAllowsMultipleSelection:NO];
result = [theOpenPanel runModalForTypes:theFileTypes];
```

3. Use the initWithContentsOfFile method of NSSound to load the sound (represented by theFileName) that the user selected in NSOpenPanel.

Because you restricted the user to opening only one audio file, its path resides in the first element of the array that NSOpenPanel returns.

```
theFiles = [theOpenPanel filenames];
theFileName = [theFiles objectAtIndex:0];
NSSound \*theSound = [[NSSound alloc] initWithContentsOf
file:theFileName byReference:YES];
```

4. Play the sound as usual:

```
[theSound play];
```

The preceding example limited the user to only one audio file selection in the NSOpenPanel. Depending on your application’s needs, you may want to permit a user to select multiple audio files in the NSOpenPanel. To do so, you need to first permit multiple selections in theOpenPanel:

```
[theOpenPanel setAllowsMultipleSelection:YES];
```

After the user clicks the OK button in the NSOpenPanel, loop through all the selected audio files in the resulting theFiles array:

```
theFiles = [theOpenPanel filenames];
int i;
for (i=0;i<[theFiles count];i++) {
theFileName = [theFiles objectAtIndex:0];
//do something with the file located at this path:
theFileName
}
```

![](bbox=[0.13, 0.531, 0.23, 0.618])