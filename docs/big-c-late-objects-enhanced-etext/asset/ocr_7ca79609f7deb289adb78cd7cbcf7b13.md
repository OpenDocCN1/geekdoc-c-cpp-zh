2. Draw two pictures next to each other.

![](bbox=[0.26, 0.12, 0.42, 0.21])

3. Draw two pictures with a gap between them.

![](bbox=[0.26, 0.28, 0.42, 0.37])

4. Draw all pictures in a long row.

![](bbox=[0.26, 0.44, 0.92, 0.5])

5. Draw a row of pictures until you run out of room, then put one more picture in the next row.

![](bbox=[0.26, 0.61, 0.62, 0.72])

Let's get started with this plan.

1. The purpose of the first step is to become familiar with the Picture type. As it turns out, the pictures are in files a.png ... t.png. Let's load the first one:

```
Picture pic("a.png");
pic.save("gallery.png");
```

That's enough to produce the picture.

![](bbox=[0.26, 0.98, 0.38, 1.0])

2. Now let's put the next picture after the first. We need to position it at the rightmost x-coordinate of the preceding picture.

![](bbox=[0.26, 0.95, 0.6, 1.0])

```
Picture pic("a.png");
Picture pic2("b.png");
pic.add(pic2, pic.width(), 0);
```