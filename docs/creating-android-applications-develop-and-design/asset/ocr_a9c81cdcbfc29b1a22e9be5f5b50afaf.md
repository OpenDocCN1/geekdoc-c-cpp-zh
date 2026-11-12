+   - Try not to move views around in your activity's java code.
+   
+     Your activity shouldn't try to change the position of things onscreen. While in portrait mode, the button might be at point (330, 120); it will be somewhere totally different in landscape mode. In this situation, adding more screen layouts will require also adding the corresponding movement code to your activity, and this can become time consuming.

# BE CAREFUL

Debugging layout issues across many linked layout files can be exhausting (I've done it), so keep your layouts as stretchy and dynamic as you possibly can. If your designs are done well, they should be able to automatically handle many screen resolutions with good use of linear and relative layouts. Fall back on includes and multiple layout folders only when dynamic layouts can't do the job. There will be times, however, when one layout doesn't do all screens justice. When this happens, make your breakouts as small and efficient as possible. Don't hesitate to use this amazing layout tool, but be careful not to use it too much.