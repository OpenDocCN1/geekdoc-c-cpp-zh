```
```cpp
if (!didInit)
    Init();
return global_userDatas[id].health;
}
public int GetLives(int id)
{
    if (!didInit)
        Init();
    return global_userDatas[id].lives;
}
public void SetLives(int id, int num)
{
    if (!didInit)
        Init();
    global_userDatas[id].lives = num;
}
public void AddLives(int id, int num)
{
    if (!didInit)
        Init();
    global_userDatas[id].lives += num;
}
public void ReduceLives(int id, int num)
{
    if (!didInit)
        Init();
    global_userDatas[id].lives -= num;
}
public void AddHealth(int id, int num)
{
    if (!didInit)
        Init();
    global_userDatas[id].health += num;
}
public void ReduceHealth(int id, int num)
{
    if (!didInit)
        Init();
    global_userDatas[id].health -= num;
}
public void SetHealth(int id, int num)
{
    if (!didInit)
        Init();
    global_userDatas[id].health = num;
}
public bool GetIsFinished(int id)
{
    if (!didInit)
        Init();
    return global_userDatas[id].isFinished;
}
public void SetType(int id, int theType)
{
    if (!didInit)
        Init();
    global_userDatas[id].type = theType;
}
public int GetType(int id)
{
    if (!didInit)
        Init();
    return global_userDatas[id].type;
}
public void SetIsFinished(int id, bool aVal)
```
```