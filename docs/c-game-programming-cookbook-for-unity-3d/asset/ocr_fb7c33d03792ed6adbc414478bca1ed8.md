```
// drop out of the race scene completely in 10
// seconds...
Invoke("FinishRace", 10);
}

void FinishRace()
{
    Application.LoadLevel("menu_MVD");
}

void ShowCount1()
{
    count1.SetActive(true);
    count2.SetActive(false);
    count3.SetActive(false);
}
nvoid ShowCount2()
{
    count1.SetActive(false);
    count2.SetActive(true);
    count3.SetActive(false);
}
nvoid ShowCount3()
{
    count1.SetActive(false);
    count2.SetActive(false);
    count3.SetActive(true);
}
nvoid HideCount()
{
    count1.SetActive(false);
    count2.SetActive(false);
    count3.SetActive(false);
}

public void UpdateWrongWay (bool isWrongWay)
{
    if (isWrongWay==oldIsWrongWay)
        return;

    if (isWrongWay)
    {
        wrongSign.SetActive(true);
    }
    else
    {
        wrongSign.SetActive(false);
    }

    oldIsWrongWay=isWrongWay;
}

public void PlayerHit(Transform whichPlayer)
{
    // tell our sound controller to play an explosion sound
    BaseSoundController.Instance.PlaySoundByIndex(1,
    whichPlayer.position);
}
```