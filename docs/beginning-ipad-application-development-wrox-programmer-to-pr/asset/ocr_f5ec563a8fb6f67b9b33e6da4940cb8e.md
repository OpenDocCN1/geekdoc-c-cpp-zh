Chapter 6 discusses screen rotations in more detail.

> > **NOTE** It's important that iPad applications support all the Landscape and Portrait display modes. Hence, it is recommended that you return a YES in the `shouldAutorotateToInterfaceOrientation:` method. The preceding code snippet is only for your information.

# Views Repositioning

In the previous section, you saw that as the orientation changes, the size and positioning of the views remain. In the real world, this scenario is not desirable because it doesn't give the user a good experience while using your application. Ideally, you should reposition your views on the screen so that they change with the view orientation.

To resize your views, go to the Interface Builder, select Label view, and choose Tools ⌥ Size Inspector. Modify the Autosizing attribute of the view as shown in Figure 2-15 by clicking the various lines inside the two squares (observe carefully the various anchors that are set in the Autosizing section). This will cause the Label view to expand/contract as the view orientation changes. At the same time, the view will anchor to the top of the screen.

![](bbox=[0.1, 0.71, 0.65, 0.85])

FIGURE 2-15

Likewise, modify the Autosizing attribute of the Text Field view as shown in Figure 2-16 by clicking the various lines inside the two squares.

Finally, modify the Autosizing attribute for the Round Rect Button control as shown in Figure 2-17 by clicking the line within the two squares. This time, you are not resizing the view when the view orientation changes. Instead, you are only anchoring it to the top of the screen.