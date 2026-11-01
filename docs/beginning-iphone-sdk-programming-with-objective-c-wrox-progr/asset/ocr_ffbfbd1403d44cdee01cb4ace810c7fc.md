```
[super viewDidLoad];
}

//---when the page control's value is changed---
- (void) pageTurning: (UIPageControl *) pageController
{
    //---get the page number you can turning to---
    NSUInteger nextPage = [pageController currentPage];
    switch (nextPage) {
        case 0:
            [tempImageView setImage:[UIImage imageNamed:@"iMac_old.jpeg"]];
            break;
        case 1:
            [tempImageView setImage:[UIImage imageNamed:@"iMac.jpeg"]];
            break;
        case 2:
            [tempImageView setImage:[UIImage imageNamed:@"Mac8100.jpeg"]];
            break;
        case 3:
            [tempImageView setImage:[UIImage imageNamed:@"MacPlus.jpeg"]];
            break;
        case 4:
            [tempImageView setImage:[UIImage imageNamed:@"MacSE.jpeg"]];
            break;
        default:
            break;
    }

    //---switch the two imageview views---
    if (tempImageView.tag==0) { //---imageView1---
        tempImageView = imageView2;
        bgImageView = imageView1;
    }
    else { //---imageView2---
        tempImageView = imageView1;
        bgImageView = imageView2;
    }

    //---animate the two views flipping---
    [UIView beginAnimations:@"flipping view" context:nil];
    [UIView setAnimationDuration:0.5];
    [UIView setAnimationCurve:UIViewAnimationCurveEaseInOut];
    [UIView setAnimationTransition:UIViewAnimationTransitionFlipFromLeft
        forView:tempImageView cache:YES];
    [tempImageView setHidden:YES];
    [UIView commitAnimations];

    [UIView beginAnimations:@"flipping view" context:nil];
    [UIView setAnimationDuration:0.5];
    [UIView setAnimationCurve:UIViewAnimationCurveEaseInOut];
    [UIView setAnimationTransition:UIViewAnimationTransitionFlipFromRight
        forView:bgImageView cache:YES];
    [bgImageView setHidden:NO];
}
```