configurable in the Unity editor by going to the menus Edit -> Project Settings -> Quality
ed editing each quality setting as a list in the Inspector window.

The main menu class is in a script called MainMenuController.cs. It is derived from
MonoBehavior and looks like this:

```
using UnityEngine;
using System.Collections;

public class MainMenuController : MonoBehaviour
{
    public int whichMenu= 0;

    public GUI킨 menuSkin;

    public string game displayName= "- DEFAULT GAME NAME -";
    public string gamePrefsName="DefaultGame";

    public string singleGameStartScene;
    public string coopGameStartScene;

    public float default_width= 720;
    public float default_height=480;

    public float audioSFXSliderValue;
    public float audioMusicSliderValue;

    public float graphicsSliderValue;
    private int detailLevels= 6;

void Start()
{
    // set up default options, if they have been saved out to
    // prefs already
    if(PlayerPrefs.HasKey(gamePrefsName+"_SFXVol"))
    {
        audioSFXSliderValue= PlayerPrefs;
        GetFloat(gamePrefsName+"_SFXVol");
    } else {
        audioSFXSliderValue=1;
    }
    if(PlayerPrefs.HasKey(gamePrefsName+"_MusicVol"))
    {
        audioMusicSliderValue= PlayerPrefs;
        GetFloat(gamePrefsName+"_MusicVol");
    } else {
        audioMusicSliderValue= 1;
    }
    if(PlayerPrefs.HasKey(gamePrefsName+"_GraphicsDetail"))
    {
        graphicsSliderValue= PlayerPrefs;
        GetFloat(gamePrefsName+"_GraphicsDetail");
    } else {
        string[] names = QualitySettings.names;
        detailLevels= names.Length;
        graphicsSliderValue=detailLevels;
    }
}
```