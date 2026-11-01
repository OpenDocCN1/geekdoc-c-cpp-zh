# WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Using the NSTimer object to create timers | Create a timer object that will call the onTimer method every half-second:
Timer = [NSTimer scheduledTimerWithTimeInterval:0.5 target:self selector:@selector(onTimer) userInfo:nil repeats:YES]; |
| Stopping the NSTimer object | [timer invalidate]; |
| Animating visual changes | [UIView beginAnimations:@some_text context:nil];
//---code with effect visual change---
[UIView commitAnimations]; |
| Performing affine transformations | Use the transform property of the view. |
| Translation | Use the CGAffineTransformMakeTranslation() function to return a CGAffineTransform data structure and set it to the transform property. |
| Rotation | Use the CGAffineTransformMakeRotation() function to return a CGAffineTransform data structure and set it to the transform property. |
| Scaling | Use the CGAffineTransformMakeScale() function to return a CGAffineTransform data structure and set it to the transform property. |
| Animating a series of images using ImageView | Set the animationImages property to an array containing UIImage objects.
Set the animationDuration property.
Set the animationRepeatCount property.
Call the startAnimating method. |