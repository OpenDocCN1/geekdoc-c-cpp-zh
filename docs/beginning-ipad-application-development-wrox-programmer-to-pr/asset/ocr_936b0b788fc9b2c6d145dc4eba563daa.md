```
[imageView addGestureRecognizer:swipeLeftGesture];
[swipeLeftGesture release];
}
    [super viewDidLoad];

//---handle swipe gesture---
-(IBAction) handleSwipeGesture:(UIGestureRecognizer *) sender {

UISwipeGestureRecognizerDirection direction =
    [(UISwipeGestureRecognizer *) sender direction];

switch (direction) {
    case UISwipeGestureRecognizerDirectionUp:
        NSLog(@"up");
        break;
    case UISwipeGestureRecognizerDirectionDown:
        NSLog(@"down");
        break;
    case UISwipeGestureRecognizerDirectionLeft:
        imageIndex++;
        break;
    case UISwipeGestureRecognizerDirectionRight:
        imageIndex--;
        break;
    default:
        break;
}

imageIndex = (imageIndex < 0) ? ([images count] - 1) :
            imageIndex % [images count];
imageView.image = [UIImage imageNamed:[images objectAtIndex:imageIndex]];
}

- (void)dealloc {
    [images release];
    [imageView release];
    [super dealloc];
}
```

+   3. Test the application on the iPhone Simulator by pressing Command-R.
+   4. Click the ImageView and drag the mouse from left to right and then from right to left. The ImageView changes its image as you swipe it with your mouse.

# How It Works

You first instantiate the images NSArray object with the names of the three images:

```
//---swipe gesture---
images = [[NSArray alloc] initWithObjects:@"architecture.jpg",
    @"Buildings.jpeg",
    @"Bridge.jpeg", nil];
```