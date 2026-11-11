With this scenario, each time a user clicks on any of the buttons on the panel, the associated listener object receives an ActionEvent that indicates a button click. In our sample program, the listener object will then change the background color of the panel.

Before I can show you the program that listens to button clicks, I need to explain how to create buttons and how to add them to a panel.

To create a button, specify a label string, an icon, or both in the button constructor. Here are two examples:

```
```java
var yellowButton = new JButton("Yellow");
var blueButton = new JButton(new ImageIcon("blue-ball.gif"));
```
```

Call the add method to add the buttons to a panel:

```
```java
var yellowButton = new JButton("Yellow");
var blueButton = new JButton("Blue");
var redButton = new JButton("Red");

buttonPanel.add(yellowButton);
buttonPanel.add(blueButton);
buttonPanel.add(redButton);
```
```

Figure 10.14 shows the result.

![](bbox=[0.272, 0.655, 0.729, 0.89])