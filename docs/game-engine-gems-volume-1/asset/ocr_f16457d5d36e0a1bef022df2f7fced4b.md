object itself.

For pointer-based devices, determining the highlighted status of a `GuiSelectable` object is achieved by passing the current on-screen cursor coordinates to the `SetFocus()` function. If, after querying the `m_HotSpot` variable, it's determined that the highlighted state should change, then the virtual `OnHighlighted()` function is called with the new desired value. Again, we can override this virtual function in derived classes to update its own state, and therefore, its visual representation.

For button-based controllers (primarily keyboards and joypads/sticks), the focus is likely to be more bespoke, perhaps being transferred by tabbing through the various highlightable components, or in the case of menus, using the directional pad on an input device. We revisit this topic later.

`GuiSelectable` objects can be told that they are not highlightable. While in this state, they are not able to become active like other `GuiComponent` objects unless explicitly made highlightable again. This is most likely to be used for components that are either just not available or are not available yet. For example, there may be a currently hidden game mode option.

Likewise, it may not be possible to actually select some items, even though they are highlightable. Perhaps, for example, moving our cursor over the currently unavailable last level on a level select screen highlights or animates that component, but the user is still not able to select it. Objects being selected have the `OnSelect()` virtual function called on them, which returns whether the selection succeeded. This is then handled by the current state.

# But What About the Menus?

Okay, so we've got the ability to place objects around the screen wherever we like, but wouldn't it be nice to put a collection of these items into a menu? Enter the `GuiSelectableGroup` class,