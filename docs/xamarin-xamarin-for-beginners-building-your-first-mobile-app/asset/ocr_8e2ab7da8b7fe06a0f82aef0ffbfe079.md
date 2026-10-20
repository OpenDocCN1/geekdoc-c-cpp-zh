We will start by creating a label from the Label class within the MainPage class builder. Labels are typically used to display text to the user. Look at the following simple code:

```
Label lblMain = new Label ();
 lblMain.Text = "Welcome to moaml Academy!";
```

We create a label and create any object of a class. We set up a new code in the previous object of the class and Label Osndnah to the variable lblMain. Then Osndna text "! Welcome to Hsoub Academy" to the Text property of the variable lblMain. The Text property is used to set and read the text content of a list.

So that we can view the previous close-on the home page of the application, we assign variable lblMain to the Content property of the class ContentPage. Since the MainPage class inherits from the ContentPage, the Content property is automatically included within it. The attribution process will be as follows:

```
this.Content = lblMain;
```

Previous attribution process is possible because the class inherits from Label Class View, which represents a general view display interface concept. Since the Content property is also of type View, this attribution is possible. The contents of the MainPage.cs file will be similar to the following: