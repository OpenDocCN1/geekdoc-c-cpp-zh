```
touchPoint.x < imageView.frame.origin.x +
imageView.frame.size.width &&
touchPoint.y > imageView.frame.origin.y &&
touchPoint.y <imageView.frame.origin.y +
imageView.frame.size.height) {
    [imageView setCenter:touchPoint];
} break;

//---double-touch---
case 2: {
    //---get info of first touch---
    UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
    //---get info of second touch---
    UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];
    
    //...
    //...
} break;
}
```

![](bbox=[0.1, 0.55, 0.95, 0.9])