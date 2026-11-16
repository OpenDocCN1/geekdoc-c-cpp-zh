![](bbox=[0.103, 0.092, 0.783, 0.576])

Figure 10.14
Scale Up Image Example.
© 2014 Timothy Wright.

The ScaleUpImageExample, as seen in Figure 10.14 and located in the javagames.images package, is just like the previous example, except that a small image is generated and it is scaled up to a much larger size. Notice that some of the methods that produce the best looking images when shrinking them do not perform the same when the image grows.

The Bilinear step-down method is good for scaling the images down, and the regular Bilinear approach for up-scaling would be my choice. But it all depends on the situation and the images. If the slower methods are performed only at startup and never again, it may be worth it to take the speed hit when loading the resource.

```
package javagames.images;
import java.awt.*;
```