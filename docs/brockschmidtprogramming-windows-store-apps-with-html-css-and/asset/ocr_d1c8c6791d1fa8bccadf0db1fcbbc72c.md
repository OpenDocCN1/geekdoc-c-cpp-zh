animate any other positional properties, the animations will run on the UI thread and likely perform poorly on lower-end hardware such as ARM devices.

# Panning Snap Points and Limits

If you run the HubPage example and pan around a bit using inertial touch gestures (that is, those that continue panning after you've released your finger, explained more in Chapter 12), you'll notice that panning can stop in any position along the way. You or your designers might like this, but it also makes sense in many scenarios to automatically stop on a section or group boundary. This can be accomplished for touch interactions using CSS styles for *snap points* as described in the following table. These are styles that you add to a pannable element alongside `overflow` styles; otherwise they have no effect. Documentation for these (and some others) can be found on the CSS reference for [touch](#). [Zooming and Panning](#). Be clear that snap points are a touch-only feature (including touchpads); if you want to provide the same kind of behavior with mouse or/and keyboard input, you'll need to do such work manually along the lines of how the FlipView control handles transition between items.

| Style | Description | Value Syntax |
|---|---|---|
| `-ms-scroll-snap-points-x` | Defines snap points along the x-axis | `snapInterval(start<length>, step<length>)`<br>`snapList(<list<length>>)` |
| `-ms-scroll-snap-type` | Defines what type of snap points should be used for the element: `none` turns off snap points, `mandatory` always adjusts panning to land on a snap point (which includes ending inertial panning), and `proximity` changes the panning only if a panning motion naturally ends "close enough" to a snap point. Using `mandatory`, then will enforce a one section/column-at-a-time panning behavior; `proximity` would pan past interim snap points if enough inertia is applied. Note also that dragging with a finger (not using an inertia gesture) will allow the user to pan directly past snap points. | `none` \| `proximity` \| `mandatory` |
| `-ms-scroll-snap-x` | Shorthand to combine `-ms-scroll-snap-type` and `-ms-scroll-snap-points-x` | `<ms-scroll-snap-type> <ms-scroll-snap-points-x>` |
| `-ms-scroll-snap-y` | Shorthand to combine `-ms-scroll-snap-type` and `-ms-scroll-snap-points-y` | `<ms-scroll-snap-type> <ms-scroll-snap-points-y>` |

In the table, `<length>` is a floating-point number, followed by an absolute units designator (`cm`, `mm`, `in`, `pt`, or `pc`) or relative units designator (`em`, `ex`, or `px`).

To add snap points for each of our hub sections in the Hub Page example, then, we only need to add two snap points styles after `overflow-x`:

```
```
.homepage section[role=main] {
    overflow-x: auto;
    -ms-scroll-snap-type: mandatory;
    -ms-scroll-snap-points-x: snapList(0px, 670px, 1045px, 1715px, 2385px, 3055px);
}
```
```