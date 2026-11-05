```
// special abilities etc.?
myID = anID;
}
public virtual void SetupDataManager()
{
    // if a player manager is not set in the
    editor, let's try to find one
    if (_myDataManager == null)
        _myDataManager =
        GetComponent<BaseUserManager>();
    if (_myDataManager == null)
        _myDataManager =
        gameObject.AddComponent<BaseUserManager>();
    if (_myDataManager == null)
        _myDataManager =
        GetComponent<BaseUserManager>();
    if (!disableAutoPlayerListAdd)
    {
        // add the player (set up data) to
        the ScriptableObject we use to store player info
        myID = _myDataManager.AddNewPlayer();
        _myDataManager.SetName(myID, "Player");
        _myDataManager.SetHealth(myID, 3);
    }
}
public virtual void AddScore(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.AddScore(myID, anAmount);
}
public virtual void AddHealth(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.AddHealth(myID, anAmount);
}
public virtual void ReduceScore(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.ReduceScore(myID, anAmount);
}
public virtual void ReduceHealth(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.ReduceHealth(myID, anAmount);
}
public virtual void SetLives(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.SetLives(myID, anAmount);
}
```