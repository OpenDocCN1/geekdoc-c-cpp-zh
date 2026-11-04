11. [Graphics, Games, Hard] Copy the program you wrote for Exercise 10 and modify it so it displays three worms with different colors. Hints:

+   - Store the worms' brushes in an array of Brush objects.
+   - Store the lists of worm positions in an array of lists of Point objects (List<Point>[]).
+   - Before you use the List<Point>[], you need to initialize it with the new keyword.
+   - Before you use a list inside the List<Point>[], you need to initialize it with the new keyword.

12. [Games] Copy the program you built for Exercise 9. The program uses the following code to display the high scores on the HighScoreForm:

```
```csharp
// Display the high scores.
HighScoresForm highScoresForm = new HighScoresForm();
highScoresForm.nameLabel0.Text = HighScoreNames[0];
highScoresForm.nameLabel1.Text = HighScoreNames[1];
highScoresForm.nameLabel2.Text = HighScoreNames[2];
highScoresForm.nameLabel3.Text = HighScoreNames[3];
highScoresForm.nameLabel4.Text = HighScoreNames[4];

highScoresForm.scoreLabel0.Text = HighScores[0].ToString();
highScoresForm.scoreLabel1.Text = HighScores[1].ToString();
highScoresForm.scoreLabel2.Text = HighScores[2].ToString();
highScoresForm.scoreLabel3.Text = HighScores[3].ToString();
highScoresForm.scoreLabel4.Text = HighScores[4].ToString();
```
```

Modify the program so it uses two for loops instead. (Hints: Use two arrays holding the form's controls. You'll have to make the change in two places.)

> > NOTE Please select the videos for Lesson 19 online at www.wrox.com/go/csharp24hourtrainer2videos.