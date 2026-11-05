instantly destroyed by the engine as soon as the game starts (is this a bug? I have no idea, but this was the only way to stop Unity eating my players!).

```
```
    // grab a reference to the player script through the
new transform we just instantiated
    BlasterPlayer _aPlayerScript =
_thePlayer.GetComponent<BlasterPlayer>();

    // assign ID to this player from the player list
    _aPlayerScript.SetPlayerDetails( _playerInfo[i].id );

    _playerScripts.Add(_aPlayerScript);
if(i==0)
        _thePlayerScript = _aPlayerScript;
}
```
```

Next, we set the ID number of our player on its BlasterPlayer Component to match up with the ID from the BaseUserManager player List. To do this, we start out by getting a reference to BlasterPlayer with GetComponent(), above, to hold in the locally scoped _playerScript variable. It is locally scoped because we only need it temporarily, during the setup.

With _playerScript in place, SetPlayerDetails() is called and we pass in the ID number from the _playerInfo List. _playerScript is then added to the _playerScripts List so that we always keep a List of players in the game - making access to their BlasterPlayer Components convenient.

To finish this function, if this is the first player we assume that the player we will follow with the Camera and track the score and lives values of, so we check if the loop variable i is equal to zero and, if it is, grab a reference to this player's BlasterPlayer Component (in _aPlayerScript) and store it in _thePlayerScript.

The curly bracket at the end of the code above signifies the end of the loop (looping through the List of UserData objects in _playerInfo).

```
```
    // set the score display
_uiManager.UpdateScoreUI(_thePlayerScript.
GetScore());
    _uiManager.UpdateLivesUI(_thePlayerScript.
GetLives());

    BaseCameraController theCam =
FindObjectOfType<BaseCameraController>();
    _theCam.SetTarget(_thePlayerScript.transform);

    // clear out the object.
    _playerInfo = null;
}
```
```

Above, we update the score, and live user interface displays by calling their respective functions in the BlasterUIManager class (see Section 12.2.6 for a breakdown of that script). To get the values we use GetScore() and GetLives() functions on the _thePlayerScript (BlastPlayer class) object.

We need to tell the Camera script what to follow here, too, and we get to it by setting up a locally scoped variable theCam of type BaseCameraController and then use FindObjectsOfType() to get Unity to go off and search for it. With a reference set up in theCam, we can call BaseCameraController.SetTarget() and pass in the target of our player's Transform.