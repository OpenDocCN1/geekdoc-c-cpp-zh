

```csharp
public void InitNewBattle()
{
    // 初始化我们准备好放入对象的哈希表
    battlePositions=new Hashtable();
    battleFinished=new Hashtable();
    battleControllers=new Hashtable();
    sortedPositions=new Hashtable();

    currentID=0;
    numberOfBattlers=0;
}
```

```csharp
public int GetUniqueID(BattleController theBattleController)
{
    // 每当请求 ID 时，我们就增加 ID 计数器。
    // 此值永远不会重置，因此它应该
    // 返回一个唯一的 ID（注意：这些 ID 对于每场战斗都是唯一的）
    currentID++;

    // 现在为这个新玩家设置一些默认数据
    if(battlePositions==null)
        InitNewBattle();

    // 这个玩家将位于最后一个位置
    battlePositions.Add(currentID, battlePositions.Count + 1);

    // 存储战斗控制器的引用，以便以后通信
    battleControllers.Add (currentID, theBattleController);

    // 默认完成状态
    battleFinished[currentID]=false;

    // 增加我们的计数器，这样当我们需要时，
    // 就不必进行任何计数或查找
    numberOfBattlers++;

    // 将此 ID 传回供战斗控制器使用
    return currentID;
}
```

```csharp
public void SetBattlePosition(int anID, int aPos)
{
    if(battlePositions.ContainsKey(anID))
    {
        // 我们在战斗位置表中
        // 已有一个条目，所以让我们修改它
        battlePositions[anID]=aPos;
    }
    else 
{
        // 我们还没有关于这个玩家的数据，所以让我们将其
        // 添加到 battlePositions 哈希表
        battlePositions.Add(anID, aPos);
    }
}
```

```csharp
public int GetBattlePosition(int anID)
{
    // 仅返回 battlePositions 哈希表中
    // 该 ID 的条目
    return (int)battlePositions[anID];
}

private string posList;
private int whichPos;

public string GetPositionListString() {
    // 此函数构建一个包含玩家列表的字符串，
    // 按照他们的得分位置排序
    // 我们遍历每个战斗者并检查其
    // 位置，并构建一个可以使用位置作为
    // 索引来访问的哈希表
    for (int b = 1; b < numberOfOfBattlers; b++) {
        whichPos= GetPosition( b );
        tempRC = (BattleController) battleControllers [b];
        sortedPositions[whichPos] = tempRC.GetID();

        if(sortedPositions.Count<numberOfOfBattlers) {
            return "";
        }

        posList="";
        // 现在我们有一个已填充的 sortedPositions 哈希表，让我们
        // 遍历它并构建字符串
        for (int b = 1; b <= numberOfOfBattlers; b++) {
            whichPos=(int)sortedPositions[b];
            posList=posList+b.ToString()+". PLAYER "+whichPos+";";
        }
        return posList;
    }

public int GetPosition ( int ofWhichID ) {
    // 首先，让我们确保我们已经准备就绪（
    // 哈希表可能还没有设置好，所以最好
    // 安全起见并这个检查
    if(battleControllers==null) {
        Debug.Log("GetPosition battleControllers is NULL!");
        return -1;
    }

    if(battleControllers.ContainsKey(ofWhichID)==false) {
        Debug.Log("GetPosition says no battle controller found for id "+ofWhichID);
        return -1;
    }

    // 首先，我们需要找到该玩家
    focusPlayerScript=(BattleController) battleControllers[ofWhichID];

    // 从假设玩家在最后
    // 开始向上计算
    myPos = numberOfBattlers;
    for (int b = 1; b < numberOfOfBattlers; b++) {
        // 假设我们在玩家后面
        isAhead = false;

        // 获取“其他”玩家的临时引用
        tempRC = (BattleController) battleControllers[b];

        // 如果 tempRC 为空（示例中）
        // 这里跳过此迭代
        if(tempRC==null)
            continue;
    }
    if (focusPlayerScript.GetID() != tempRC.GetID())
    { // 确保我们不是在尝试比较
        // 检查此玩家是否击中了
        if (focusPlayerScript.howMany_fragged > tempRC.howMany_fragged)
        {
            isAhead=true;
            // 另一个版本，纯属好玩……
            // 击中次数
            if (focusPlayerScript.howMany_fragged == tempRC.howMany_fragged &&
                focusPlayerScript.GetID() == tempRC.GetID())
            { // 所以使用 id 来排序
                // 他们
                isAhead=true;
            }
        }
    }

    if ( isAhead)
    {
        myPos--;
    }
    return myPos;
}

public void StartBattle() {
    battleRunning=true;
    UpdateBattleStates();
}
public void StopBattle() {
    // 我们不想反复告诉他们战斗
    // 结束，如果我们已经调用过了，所以
    // 首先检查 battleRunning 是否真
    if(battleRunning==true) {
        // 设置标志以停止重复调用
        battleRunning=false;

        // 告诉大家关于 battleRunning 的更新
        UpdateBattleStates();

        // 告诉所有玩家我们结束了，
        // 通过向每个带有战斗
        // 控制器的对象发送消息
        // 调用控制脚本中的 PlayerFinishedBattle() 函数
        for ( int b = 1; b <= numberOfBattlers; b++) {
            tempRC = (BattleController) battleControllers[b];
            tempRC.gameObject.SendMessage("PlayerFinished Battle", SendMessage.DontRequireReceiver);
        }
    }
}
public void RegisterFrag(int whichID) {
    focusPlayerScript=(BattleController) battleControllers[whichID];
    focusPlayerScript.FraggedOther();
}
void UpdateBattleStates() {
    for ( int b = 1; b <= numberOfBattlers; b++) {
        tempRC = (BattleController) battleControllers [b];
        tempRC.UpdateBattleState(battleRunning);
    }
}
```

