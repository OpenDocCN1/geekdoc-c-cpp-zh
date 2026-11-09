| Constant name | Attributes |
|---|---|
| QUIT | none |
| ACTIVEEVENT | gain, state |
| KEYDOWN | , key, mod |
| KEYUP | key, mod |
| MOUSEMOTION | pos, rel, buttons |
| MOUSEBUTTONUP | pos, button |
| MOUSEBUTTONDOWN | pos, button |

# Keyboard events

KEYUP and KEYDOWN events have attribute key constants representing keyboard keys.
Using capital k followed by underscore and key name,
For example F1 is K_F1, w is K_w.
In this snippet, we check when a key is pressed down using pygame.KEYDOWN, we check what arrow key is pressed down and print a message for key name.

```
```python
for event in pygame.event.get():
    if event.type == pygame.QUIT:
        pygame.quit()
    elif event.type == pygame.KEYDOWN:
        if event.key == pygame.K_UP:
            print("Player moved up")
        elif event.key == pygame.K_LEFT:
            print("Player moved left")
        elif event.key == pygame.K_DOWN:
            print("Player moved down")
        elif event.key == pygame.K_RIGHT:
            print("Player moved right")
```
```