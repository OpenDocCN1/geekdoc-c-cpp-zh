```
void StartRunning()
{
    isRunning = true;
    runSpeed = 1f;
    distanceCounter = 1f;

    SetTargetState(Game_State_gameStarted);

    // start animation
    _RunManCharacter.StartRunAnimation();

    InvokeRepeating("AddScore", 0.5f, 0.5f);
}

void EndGame()
{
    // stop running
    isRunning = false;
    runSpeed = 0;

    // schedule return to main menu in 4 seconds
    Invoke("ReturnToMenu", 4f);

    // stop the repeating invoke that awards score
    CancelInvoke("AddScore");

    // let's try to store the high score (profile manager takes care of checking if it's a high score or not, we just submit a score)
    if (GetComponent<BaseProfileManager>().SetHighScore(_RunManCharacter.GetScore()) == true)
        uiManager.ShowGotHighScore();

    // update final score ui
    uiManager.SetFinalScore(_RunManCharacter.GetScore());

    // update target state
    SetTargetState(Game_State_gameEnded);
}

void AddScore()
{
    _RunManCharacter.AddScore(1);
}

void ReturnToMenu()
{
    SceneManager.LoadScene("RunMan_menu");
}

public void PlayerFell()
{
    SetTargetState(Game_State_gameEnding);
}

void SpawnPlatform()
{
    runSpeed += 0.02f;
    distanceCounter = 0;
    float randomY = Random.Range(playAreaTopY, playAreaBottomY);
    Vector2 startPos = new Vector2(platformStartX, randomY);
    Instantiate(_platformPrefab, startPos, Quaternion.identity);
}
```