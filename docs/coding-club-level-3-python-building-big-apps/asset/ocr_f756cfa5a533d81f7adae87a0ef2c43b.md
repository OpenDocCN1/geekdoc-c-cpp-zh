# # The Bat class planning page

On this page we are going to build a bat factory that can produce a left or right bat so let’s get designing:

![](bbox=[0.274, 0.222, 0.437, 0.492])

![](bbox=[0.57, 0.221, 0.748, 0.785])

# ## Notes

The first seven Bat-class attributes should be fairly obvious as they are similar to the Ball class (which is also created in a box). We also need a rectangle to be the bat and a table object for the bat to move on. The interesting attributes are the speed attributes:

`y_speed`

The bat’s movement will be attached to a key press. The speed is simply the number of pixels it can jump for each press of the key. So y_speed will be set to a default of 23 pixel jumps (which seems to work well).