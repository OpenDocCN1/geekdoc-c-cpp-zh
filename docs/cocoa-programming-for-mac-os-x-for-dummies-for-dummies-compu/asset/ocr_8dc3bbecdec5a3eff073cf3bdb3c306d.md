+   5. **Select the `MyAudioController` class and open the Identity Inspector by choosing Tools:\Identity Inspector. Add three actions to the `MyAudioController` class by clicking the + button at the bottom of the Class Actions section.**
Name the actions `playAppSound:`, `playSoundFile:`, and `playSystemSound:`.

+   6. **Create the header and implementation files in Xcode.**
Select the `MyAudioController` class and choose File:\Write Class Files. Don't worry about connecting the actions in Interface Builder yet; you'll do that later.

+   7. **Return to Xcode and drag an AIFF file from Finder to your project.**
Make sure that the AIFF file is `banjo.aiff` or modify the code to match whatever filename you choose.

+   8. **Navigate to the `MyAudioController.m` file and add the following code:**

```
```objectivec
#import "MyAudioController.h"

@implementation MyAudioController

- (IBAction)playAppSound: (id) sender
{
    //play a sound file that is part of the project
    NSSound *theSound = [NSSound soundNamed:@"banjo"]; 
    [theSound play];
}

- (IBAction)playSoundFile: (id) sender
{
    int result;
    NSArray *theFiles;
    NSString *theFileName;

    //fill an array with all
    //of the file types that Cocoa can use
    NSArray *theFileTypes = [NSSound
    soundUnfilteredFileTypes];

    //display the sound file types in the console
    int i;
    for (i=0; i<[theFileTypes count]; i++)
        NSLog([theFileTypes objectAtIndex:i]);

    //create and display an open panel
    NSOpenPanel *theOpenPanel = [NSOpenPanel
    openPanel];
```
```