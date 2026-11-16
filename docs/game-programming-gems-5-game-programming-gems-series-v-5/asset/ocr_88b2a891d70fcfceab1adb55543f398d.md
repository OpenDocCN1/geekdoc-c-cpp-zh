The following pseudocode shows how the tracking of the smooth sections is handled. We iterate through the keys and either set given speeds or set up parameters for the smooth sections. A Boolean inSmooth is used to indicate whether we're currently tracking a smooth section.

```
inSmooth = false
for each key do
    if current in-speed is not smooth
        if inSmooth
            finish clamped spline
            inSmooth = false
        else
            set given speed
    else if inSmooth
        start clamped spline
        inSmooth = true
    if not at end and out key is smooth
        add to middle of smooth spline
    else
        finish natural spline
        inSmooth = false
if current out-speed is not smooth
    set given speed
else if inSmooth
    start natural spline
    inSmooth = true
```

Some details have been skipped here for clarity. For example, we don't consider the in-speed for the first key or the out-speed for the last key, as they're not valid. The full details can be found in the sample code.

# Example

As an example, let's assume that the user has set three time-distance pairs, with the following speed parameters:

| Time | Distance | In-Speed | Out-Speed |
|---|---|---|---|
| 0.0 | 0.0 | — | Linear |
| 0.45 | 0.60 | Fast | Smooth |
| 1.0 | 1.0 | Slow | — |

The outgoing speed at the first key is linear, so its value is (0.6-0.0)/(0.45-0.0), however, we correct this by multiplying by (0.45-0.0), so the final stored speed is 0.6. The incoming speed at the second key is fast-out, so its value is 3(0.6-0.0). The outgoing speed at the second key is smooth, so we start building a linear system. In this simple example, we stop building it immediately at the next key since it is slow-in and thus non-smooth. Our linear system for this section of curve looks like Equation 2.3.7.