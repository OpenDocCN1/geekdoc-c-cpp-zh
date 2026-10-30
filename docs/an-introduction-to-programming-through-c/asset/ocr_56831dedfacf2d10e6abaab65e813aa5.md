Remember that char data is really numerical, so it is perfectly acceptable to compare it using the operator ==. This program will execute 100 user commands to move the turtle before stopping. Try it!

# 6.4.1 “Buttons” on the canvas

We can build “buttons” on the canvas using the Rectangle shapes of Section 5.3. We can control the turtle by clicking on the buttons. This gives yet another turtle controller.

```
main_program{
    initCanvas();

    const float bFx=150,bFy=100, bLx=400,bLy=100, bWidth=150,bHeight=50;
    Rectangle buttonF(bFx,bFy,bWidth,bHeight), buttonL(bLx,bLy,bWidth,bHeight);

    Text tF(bFx,bFy,"Forward"), tL(bLx,bLy,"Left Turn");
    Turtle t;

    repeat(100){
        int clickPos = getClick();
        int cx = clickPos/65536;
        int cy = clickPos % 65536;

        if(bFx-bWidth/2<= cx && cx<= bFx+bWidth/2 &&
            bFy-bHeight/2 <= cy && cy <= bFy+bHeight/2) t.forward(100);

        if(bLx-bWidth/2<= cx && cx<= bLx+bWidth/2 &&
            bLy-bHeight/2 <= cy && cy <= bLy+bHeight/2) t.left(10);
    }
}
```

The program begins by drawing the rectangles on the screen. Notice that we have not given the coordinate information of the buttons by writing numbers directly, but first created the names bFx,bFy and so on having specific values and then used these names in the button creation. Using such names is convenient: if you want to adjust the layout of buttons later, you just need to change the value of some name. Without names, you would have needed to make changes in every place the number appeared. In the present case, if you want to change the width of the rectangles, you just need to assign a different value to bWidth, instead of worrying in which all places the width value needs to be changed.

Next, text is put in the rectangles. Then we go into a loop. Inside, we wait for the user to click. We check whether the click is inside either of the two rectangles. This is done in the two if statements in the loop. Each check has two parts: we must check if the x coordinate of the click is between the left edge of the rectangle and the right edge, i.e. the left edge