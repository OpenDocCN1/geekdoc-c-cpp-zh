![](bbox=[0.13, 0.07, 0.85, 0.39])

FIGURE 26.1: This screen shot shows the output of the cell simulation drawable. The properties that are used are visible on the left side of the window.

handling, such as rendering the particles or the application of non-collisional forces like gravity, can be performed. This type of handling can also be performed by breaking out of the event-handling loop occasionally. With some minor modifications, we can make it so that the DrawBouncingBalls class we wrote previously works in this way.

The first modification we have to make is not to the bouncing balls, but to our queue. Unlike the other examples that have been mentioned, this example requires that we are able to remove events from the queue without processing them. Each time we process an event that modifies the velocity of a particle, all future events involving that particle must be removed. The most general way for us to add that functionality is with a method like the following.

```
def removeMatches(f: A => Boolean) {
  var rover = end.next
  while(rover!=end) {
    if(f(rover.data)) {
      rover.prev.next = rover.next
      rover.next.prev = rover.prev
    }
    rover=rover.next
  }
}
```

This takes a predicate function and removes all the elements for which the function is true.

With this added in, we can make modifications to DrawBouncingBalls itself. We will show the entire class here as more has been modified or added than was left alone.

```
package scalabook.drawing
```

```
import java.awt.{Graphics2D,Color}
```