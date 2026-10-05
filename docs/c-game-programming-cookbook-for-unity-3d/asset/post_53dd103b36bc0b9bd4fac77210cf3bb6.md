
```cpp
ConfirmExitGame();
}
// End the group started above. This is very
// important to remember!
GUI.EndGroup();
break;
case 1:
    // Options menu
    GUI.BeginGroup(new Rect (native_width / 2 - 150,
    native_height / 2 - 250, 500, 500));
    // Are you sure you want to exit?
    GUI.Label(new Rect(0, 50, 300, 50 ), "OPTIONS", "textarea");
    if(GUI.Button(new Rect(0, 250, 300, 40 ), "AUDIO OPTIONS"))
    {
        ShowAudioOptionsMenu();
    }
    if(GUI.Button(new Rect(0, 300, 300, 40 ), "GRAPHICS OPTIONS"))
    {
        ShowGraphicsOptionsMenu();
    }
    if(GUI.Button(new Rect(0, 400, 300, 40 ),"BACK TO MAIN MENU"))
    {
        GoMainMenu();
    }
    GUI.EndGroup();
    break;
case 2:
    GUI.BeginGroup(new Rect (default_width / 2 - 150,
    default_height / 2 - 250, 500, 500));
    // Are you sure you want to exit?
    GUI.Label(new Rect(0, 50, 300, 50 ), "Are you sure you to exit?", "textarea");
    if(GUI.Button(new Rect(0, 250, 300, 40 ),"YES, QUIT PLEASE!"))
    {
        ExitGame();
    }
    if(GUI.Button(new Rect(0, 300, 300, 40 ), "NO, DON'T QUIT"))
    {
        GoMainMenu();
    }
    GUI.EndGroup ();
break;

case 3:
    // AUDIO OPTIONS
    GUI.BeginGroup(new Rect (default_width / 2 - 150,
    default_height / 2 - 250, 500, 500));
    GUI.Label(new Rect (0, 50, 300, 50), "AUDIO OPTIONS", "textarea");
    GUI.Label(new Rect (0, 170, 300, 20), "SFX volume:");
    audioSFXSSiderValue = GUI.HorizontalSlider (new
    Rect (0, 200, 300, 50), audioSFXSSiderValue, 0.0f, 1f);
    GUI.Label(new Rect (0, 270, 300, 20), "Music volume:");
    audioMusicSliderValue = GUI.HorizontalSlider (new
    Rect (0, 300, 300, 50), audioMusicSliderValue, 0.0f, 1f);

    if (GUI.Button(new Rect (0, 400, 300, 40), "BACK TO OPTIONS MENU"))
    {
        SaveOptionsPrefs();
        ShowOptionsMenu();
    }
    GUI.EndGroup ();
    break;

case 4:
    // GRAPHICS OPTIONS
    GUI.BeginGroup(new Rect (default_width / 2 - 150,
    default_height / 2 - 250, 500, 500));
    GUI.Label(new Rect (0, 50, 300, 50), "GRAPHICS OPTIONS", "textarea");
    GUI.Label(new Rect (0, 170, 300, 20), "Graphics quality:");
    graphicsSliderValue = Math.RoundToInt(GUI.
    HorizontalSlider(new Rect (0, 200, 300, 50), 
    graphicsSliderValue, 0, detailLevels));

    if (GUI.Button(new Rect (0, 400, 300, 40), "BACK TO OPTIONS MENU"))
    {
        SaveOptionsPrefs();
        ShowOptionsMenu();
    }
    GUI.EndGroup ();
    break;

} // - end switch
void LoadLevel( string whichLevel ) {
    Application.LoadLevel(whichLevel);
}
void GoMainMenu() {
    whichMenu=0;
}
void ShowOptionsMenu() {
    whichMenu=1;
}
void ShowAudioOptionsMenu() {
    whichMenu=3;
}
void ShowGraphicsOptionsMenu() {
    whichMenu=4;
}
void SaveOptionsPrefs() {
    PlayerPrefs.SetFloat(gamePrefsName+"__SFXVol",
    audioSFXSliderValue);
    PlayerPrefs.SetFloat(gamePrefsName+"__MusicVol",
    audioMusicSliderValue);
    PlayerPrefs.SetFloat(gamePrefsName+"__GraphicsDetail",
    graphicsSliderValue);

    // set the quality setting
    QualitySettings.SetQualityLevel((int)graphicsSliderValue,
    true);
}
void ConfirmExitGame() {
    whichMenu=2;
}
void ExitGame() {
    // tell level loader to shut down the game for us
    Application.Quit();
}
```

# 10.1.1 Script Breakdown

After all the variable declarations, the first part of this script does the initial setup within Start() function. Remember that, in Unity, the Start function is automatically called by the engine after a script is initialized and before the first update. Here, the script checks to see whether or not PlayerPrefs data have already been saved to disk. If it finds PlayerPrefs keys that exist, it loads them in and applies the saved values to our local variables. To store slider values from the options menu, there are three variables used: 

- 1. audioSFXSliderValue, a float, with a value between 0 and 1, for the sound effects volume level.
- 2. audioMusicSliderValue, a float, with a value between 0 and 1, for the music volume level.
- 3. graphicsSliderValue, an integer to store the level of graphics detail. The number acts as an index used to set Unity's QualitySettings quality level with the SetQualityLevel function.

```cpp
void Start ({
    // set default options, if they have been saved out to
    if (PlayerPrefs.HasKey(gamePrefsName+"__SFXVol")) {
        audioSFXSliderValue = PlayerPrefs.GetFloat(gamePrefsName+"__SFXVol");
    } else {
        audioSFXSliderValue = 1;
    }
    if (PlayerPrefs.HasKey(gamePrefsName+"__MusicVol")) {
        audioMusicSliderValue = PlayerPrefs.GetFloat(gamePrefsName+"__MusicVol");
    } else {
        audioMusicSliderValue = 1;
    }
    if (PlayerPrefs.HasKey(gamePrefsName+"__GraphicsDetail")) {
        graphicsSliderValue = PlayerPrefs.GetInt(gamePrefsName+"__GraphicsDetail");
    } else {
        string[] names = QualitySettings.names;
        detailLevels = names.Length;
        graphicsSliderValue = detailLevels;
    }
    // set the quality setting
    QualitySettings.SetQualityLevel((int)graphicsSliderValue, true);
}
```

When you start a Unity project and the screen resolution appears, there is a dropdown menu for the quality settings, usually along the lines of Edit -> Project Settings -> Quality. You can modify these settings in the Unity window by deleting or adding new settings as fit. This means there is no guarantee of getting the same number of quality settings from game to example, you may choose to have only Good, Bad, and Ugly. To find out how many settings are there, QualitySettings.names is used to return an array containing all available quality names, and .Length property tells how many items are in the array. This number of quality settings is held in the variable detailLevels. In the Start() function, the code to do this looks like:

```cpp
string[] names = QualitySettings.names;
detailLevels = names.Length;
```

By default, the function also uses the highest quality level as a setting when no PlayerPrefs is found.

```cpp
graphicsSliderValue = detailLevels;
QualitySettings.SetQualityLevel((int)graphicsSliderValue, true);
```

Next, we move straight to OnGUI function:

```cpp
void OnGUI()
{
    float resX = Screen.width / default_width;
    float resY = Screen.height / default_height;
    GUI.matrix = Matrix4x4.TRS(new Vector3(0, 0, 0),
    Quaternion.identity, new Vector3(resX, resY, 1));
}
```

The Matrix4x4 function is complicated, and I am not about to explain it to you (trust me, I am no mathematician!), but the simplest explanation is as follows: The default width and height are the resolution at which (if you intend the screen resolution to be 1024x768, you would make the default_width and default_height variables equal to 1024 and 768 respectively). The multipliers with GUI.matrix are established by taking the width and height of the screen and dividing it by your default width and height. The line that does all the hard work is where Unity sets GUI.matrix. It takes your values and stretches the UI to fill the screen. This means the UI will at least suit every resolution. Once the GUI.matrix is set, everything we draw in OnGUI function will be scaled accordingly so we can start drawing the menus.

To set a skin, we need to tell Unity about it in OnGUI function. You can use as many different skins as like, changing/setting the skin is easy:

```cpp
// set the GUI skin to use our custom menu
GUI.skin = menuSkin;
```

In our UI function, menuSkin is a public variable so that we can set the GUI skin value in the Inspector of the editor. The next step is to check the variable whichMenu to see "which menu" we need to render. There are four different screens we may display here, the first one the main menu (case 0):

```cpp
switch (whichMenu)
{
case 0:
```

To help us to position the menu and for the most flexibility, we will render it within a group. Using a group is similar to drawing the UI inside a window, which can be moved around its contents keeping the same layout. The coordinate system for the GUI contents within the group starts at 0,0 in the top left of the group and remains unaffected by screen positioning (which continues to be determined by the group rather than its content).

```cpp
GUI.BeginGroup(new Rect (default_width / 2 - 150, height / 2 - 250, 500, 500));
```

Putting content into a group is simple. Using GUI.BeginGroup() within an OnGUI function to start the content and GUI.EndGroup() once the content is complete.

```cpp
GUI.Label(new Rect (0, 50, 300, 50 ), displayName="textarea");
```

One way to get text onto the screen is to use UILabel. In the line above, we define a rectangle where we are going to render (keep in mind that this is happening within a group, so the coordinate system starts at 0 top left of the group). This is the name of the game, we are using a string to hold the game name called gameDisplayName. A public string in this way means we can change the game name in the Unity editor's Inspector window without having to edit the script.

The final part of the GUI.Label line is GUI. This is just a string that refers to a style defined in GUISkin. In this case, it's the style "textarea", and it makes sure when this text is rendered that it uses the correct font, size, and text alignment. The next part of the script renders and acts on a button. The code to check for a button press is all in just a single line:

```cpp
if (GUI.Button(new Rect (0, 200, 300, 40 ), "START GAME", "button"))
```

GUI.Button uses the defined rectangle to draw a button with the specified text "START GAME" in it. Again, you can see here that, to encourage predictability, we specify the Style="button". Notice that this line acts like a Boolean in this conditional statement, and if the button is pressed, everything within the curly brackets occurs:
