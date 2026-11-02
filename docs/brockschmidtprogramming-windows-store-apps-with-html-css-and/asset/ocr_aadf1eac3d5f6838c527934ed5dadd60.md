# # The Touch Language, Its Translations, and Mouse/Keyboard Equivalents

On the Windows Developer Center, the rather extensive article on Touch interaction design is helpful for designers and developers alike. It discusses various ergonomic considerations, has some great diagrams on the sizes of human fingers, provides clear guidance on the proper size for touch targets given that human reality (falling between 30px and 50px), and outlines key design principles such as providing direct feedback for touch interaction (animation) and having content follow your finger.

Most importantly, the design guidance also describes the Windows Touch Language, which contains the eight core gestures that are baked into the system and the controls. The table below shows and describes the gestures and indicates what events appear in the app for them (see the previously linked topics for videos of these gestures).

| Gesture | Meaning and Gesture Events | Description |
| --- | --- | --- |
| One finger touches the screen and lifts up. | Tap for primary action (commanding); appears as `click` and `MSGestureTap` events on the element. | Tapping on an element invokes its primary action, typically executing a command, checking a box, setting a rating, positioning a cursor, etc. |
| One finger touches the screen and stays in place. | Press and hold to learn; appears as `contextmenu` and `MSGestureHold` events on the element. | This touch interaction displays detailed information or teaching visuals (for example, a tooltip or context menu) without a commitment to an action. Anything displayed this way should not prevent users from panning if they begin sliding their finger. |
| One or more fingers touch the screen and move in the same direction. | Slide to pan (can be horizontal or vertical); automatically appears as scrolling events for scrollable regions. Also appears as a gesture series (`MSGestureStart`, `MSGestureChange`, `MSGestureEnd`, possibly with inertial gesture events signaled by `MSInertiaStart`, plus `pointer` events). | Slide is used primarily for panning interactions but can also be used for moving, drawing, or writing. Slide can also be used to target small, densely packed elements by scrubbing (sliding the finger over related objects such as radio buttons). |

![](bbox=[0.151, 0.453, 0.404, 0.584])

![](bbox=[0.151, 0.622, 0.405, 0.721])

![](bbox=[0.151, 0.762, 0.404, 0.862])