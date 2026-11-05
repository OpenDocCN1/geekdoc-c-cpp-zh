```
void Start()
{
    _scoreText.text = "Score 0";
    _newHighScoreText.gameObject.SetActive(false);
    // hide all ui canvas
    HideAll();
}
public void ShowGetReadyUI()
{
    ShowCanvas(0);
}
public void HideGetReadyUI()
{
    HideCanvas(0);
}
public void ShowGameOverUI()
{
    ShowCanvas(1);
}
public void ShowGameUI()
{
    ShowCanvas(2);
}
public void HideGameUI()
{
    HideCanvas(2);
}
public void SetScore(int scoreAmount)
{
    _scoreText.text = "Score "+scoreAmount.ToString("D5");
}
public void SetHighScore(int scoreAmount)
{
    _highText.text = "High " + scoreAmount.ToString("D5");
}
public void SetFinalScore(int scoreAmount)
{
    _finalScoreText.text = "Final Score " + scoreAmount.ToString("D5");
}
public void ShowGotHighScore()
{
    _newHighScoreText.gameObject.SetActive(true);
}
```

The first thing to notice about the code above is that it derives from a class named CanvasManager. CanvasManager is part of the framework for this book, and it provides methods for showing and hiding Canvases. To use CanvasManager, each Canvas GameObject has a Component on it named Canvas Group. Canvas Group is a Component provided by Unity that allows you to control the alpha level of an entire UI Canvas and to enable or disable interactions with it. What