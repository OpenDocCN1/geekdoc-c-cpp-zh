```
}
```

```
File.WriteAllText("highscores.csv", allHighScoresText);
```

In case this is something you have not seen before when it comes to creating a string, you can use special characters inside the string. Special characters are easy to make in a string; you just start with a \ character which indicates that the next character to be typed is a special character and not a normal one. In the above example, we put \n and, although you see two characters, this is actually just one. It is a newline character which makes the line wrap to the next one. It’s the same as what happens when you press the Enter key on your keyboard.

The reverse of this is reading the file back in and you can do a lot of similar things with it.

You can start by reading the whole text of that file back in. Next, you can parse the file; that means you break up a text block into small parts that are more meaningful. After that, the file is turned back to a list containing the high scores.

The next example will read the high scores file we created and convert it back to a list of high scores:

```
string[] highScoresText = File.ReadAllLines("highscores.csv");
```

```
HighScore[] highScores = new HighScore[highScoresText.Length];
```

```
for(int index = 0; index < highScoresText.Length; index++)
{
    string[] tokens = highScoresText[index].Split(',');

    string name = tokens[0];
```