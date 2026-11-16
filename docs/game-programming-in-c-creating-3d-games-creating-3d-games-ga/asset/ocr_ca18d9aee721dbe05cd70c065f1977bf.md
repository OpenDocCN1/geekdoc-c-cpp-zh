![](bbox=[0.17, 0.09, 0.72, 0.42])

Figure 2.6 Side-scroller project in action

The code includes an implementation of the hybrid `Actor/Component` model, `SpriteComponent`, `AnimSpriteComponent`, and parallax scrolling. It also includes a subclass of `Actor` called `Ship`. The `Ship` class contains two speed variables to control the left/right speed and the up/down speed, respectively. Listing 2.9 shows the declaration of `Ship`.

# Listing 2.9 Ship Declaration

Click here to view code image

```
```
class Ship : public Actor
{
public:
```
```