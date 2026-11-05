```
```csharp
public virtual void AddLives(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.AddLives(myID, -anAmount);
}

public virtual void ReduceLives(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.ReduceLives(myID, anAmount);
}

public virtual void SetScore(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.SetScore(myID, anAmount);
}

public virtual void SetHealth(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.SetHealth(myID, anAmount);
}

public virtual void SetName(string aName)
{
    if (!didInit)
        Init();
    _myDataManager.SetName(myID, aName);
}

public int GetLives()
{
    if (!didInit)
        Init();
    return _myDataManager.GetLives(myID);
}

public int GetHealth()
{
    if (!didInit)
        Init();
    return _myDataManager.GetHealth(myID);
}

public int GetScore()
{
    if (!didInit)
        Init();
    return _myDataManager.GetScore(myID);
}
}
}
```
```

Right away, in the code above you may notice the similarities to the BaseUserManager class. A large portion of the script above is taken up with calls to the corresponding functions in BaseUserManager – by duplicating those functions here to call out to them, we are adding all of the functionality of BaseUserManager to the player script and simplifying how we need to call it. For