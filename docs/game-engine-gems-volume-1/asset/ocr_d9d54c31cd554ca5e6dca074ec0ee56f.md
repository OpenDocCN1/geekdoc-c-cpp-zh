this requires computing the Earth's tilt for the simulated time.
Finally, we transform the equatorial coordinates into horizon
coordinates for the location on Earth that you wish to simulate. As
a finishing touch, we also apply atmospheric refraction to the
horizon coordinates, which affects the perceived location of the sun
and moon as they approach the horizon.

Care must be taken that this final transformation is consistent with
your engine's coordinate system conventions; if your users might
define "north" and "up" as any arbitrary axis, you'll want to provide
a means for them to influence this final transformation into local
coordinates. The sun rising in the West instead of the East is an
embarrassing bug that is very easy to slip through testing. You
may also want to expose geographic coordinates for the sun and
moon; instead of being relative to a specific location on the surface
of the Earth, these coordinates are relative to the center of the
Earth. Flight simulators that can cover large distances frequently
use this coordinate system, and our Ephemeris class will
compute this for you as well.

These same matrices are useful for transforming things such as
star fields in the sky. It may sound like overkill, but having
accurately positioned stars in your scenes could be important to
someone creating, for example, a navigation training application.

All this work pays off when your engine's sun and moon rise at
exactly the right time for the location being simulated. Got a game
that takes place in the winter in Alaska? Your nights will be long
and the sun will be low—automatically.