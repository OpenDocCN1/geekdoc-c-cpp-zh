```
// complex shape - reusable as a single item
public void Alien1(Graphics g, Brush bAlienColor) {
    Point[] Alien = {
        new Point(this.imagePosX-10, this.imagePosY-10),
        new Point(this.imagePosX-5, this.imagePosY-10),
        new Point(this.imagePosX-5, this.imagePosY-5),
        new Point(this.imagePosX+5, this.imagePosY-5),
        new Point(this.imagePosX+5, this.imagePosY-10),
        new Point(this.imagePosX+10, this.imagePosY-10),
        new Point(this.imagePosX+5, this.imagePosY-5),
        new Point(this.imagePosX+5, this.imagePosY-5),
        new Point(this.imagePosX+5, this.imagePosY+5),
        new Point(this.imagePosX+10, this.imagePosY+5),
        new Point(this.imagePosX+5, this.imagePosY+10),
        new Point(this.imagePosX+5, this.imagePosY+5),
        new Point(this.imagePosX-5, this.imagePosY+5),
        new Point(this.imagePosX-5, this.imagePosY+10),
        new Point(this.imagePosX-10, this.imagePosY+10),
        new Point(this.imagePosX-10, this.imagePosY+5),
        new Point(this.imagePosX-5, this.imagePosY+5),
        new Point(this.imagePosX-5, this.imagePosY-5),
        new Point(this.imagePosX-10, this.imagePosY-5),
        new Point(this.imagePosX-10, this.imagePosY-10));
    }

    g.FillPolygon(bAlienColor, Alien);
}
```

```
// complex shape - reusable as a single item
public void Alien2(Graphics g, Brush bAlienColor) {
    Point[] Alien = {
        new Point(this.imagePosX-5, this.imagePosY-10),
        new Point(this.imagePosX+5, this.imagePosY-10),
        new Point(this.imagePosX+5, this.imagePosY-5),
        new Point(this.imagePosX+10, this.imagePosY-5),
        new Point(this.imagePosX+10, this.imagePosY+10),
        new Point(this.imagePosX+5, this.imagePosY+10),
        new Point(this.imagePosX+5, this.imagePosY),
        new Point(this.imagePosX-5, this.imagePosY),
        new Point(this.imagePosX-5, this.imagePosY+10),
        new Point(this.imagePosX-10, this.imagePosY+10),
        new Point(this.imagePosX-10, this.imagePosY-5),
        new Point(this.imagePosX-5, this.imagePosY-5),
        new Point(this.imagePosX-5, this.imagePosY-10));
    }
}
```