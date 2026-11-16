the value of the input on that frame. In this chapter’s input system, you will give the option of either querying this basic value or querying for the different input states.

# Events

Recall from Chapter 1, “Game Programming Overview,” that SDL generates different events that the program can optionally respond to. Currently, you respond to the SDL_Quit event, which occurs when the player tries to close the window.
Game::ProcessInput checks every frame if there are events in the queue and can selectively choose to respond to them.

SDL also generates events for input devices. For example, every time the player presses a key on the keyboard, SDL generates an SDL_KEYDOWN event (corresponding to the Pressed button state).
Conversely, every time the player releases a key, it generates an SDL_KEYUP event (corresponding to the Released state). If you only care about positive and negative edges, then this is a very quick way to set up code to respond to these actions.

However, for the case of pressing W to move forward, this means you need extra code to track whether W is held because you only get the negative and positive edges from the SDL events. Although you can certainly design an input system entirely based around events, this chapter uses SDL events only when required (such as for