Pygame deal with user inputs mainly using pygame.event module. pygame.event listens and register all events that comes from a keyboard or mouse. Every time event happen an event object is created to record it.

In fact, we have been using pygame.event several times in our programs.

In this snippet, in game loop we continuously check for any new events pygame.event.

`pygame.event.get()` returns a list of events that occurred since the last `pygame.event.get()` call.

When the quit button is pressed pygame.event registers this event as event with a type pygame.QUIT.

So we loop through all events and check if any of the events type is pygame.QUIT if so we set loop variable to false to quit the loop in next iteration.

```
```python
# ? : game infinite loop
loop = True
while loop:
    # if quit button press quit
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = False
```
```

To read more about pygame events refer to this link:
[http://man.hubwiz.com/docset/PyGame.docset/Contents/Resources/Documents/ref/event.html](http://man.hubwiz.com/docset/PyGame.docset/Contents/Resources/Documents/ref/event.html)

This table show some of common pygame.event constant and their attributes.