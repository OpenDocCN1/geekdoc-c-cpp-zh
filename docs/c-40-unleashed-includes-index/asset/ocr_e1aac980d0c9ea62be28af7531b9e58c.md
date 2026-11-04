Location property for a table and a kid in two different rooms, where location is relative to some corner of the room. The table is positioned at position (10,10), and the kid is reading his Tintin book also at position (10,10), so the same instance of the Point type could be used for both:

```
var p = new Point(10,10); // with Point a reference type
kid.Location = p;
table.Location = p;
```

Now, what happens if the person in the first room wants to move his table to position (20,20)? Different approaches can be taken, but the aliasing property of reference types can be disadvantageous. Because the same instance of Point is used for both Location properties, changes to this very instance will affect both objects’ locations:

```
p.X += 10;
p.Y += 10;
```

I’m guessing the kid won’t be happy to be moved by some invisible teleportation force, as illustrated in Figure 9.4.

![](bbox=[0.05, 0.71, 0.9, 0.92])

FIGURE 9.4 Point as a reference type.