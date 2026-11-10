![](bbox=[0.24, 0.108, 0.757, 0.371])

**Figure 14.3**
OpenGL compositing overview.

+   2. The specified *blendEquation* is then used to combine the modified source and destination pixels to produce a new destination color. The blend equation is specified in the glBlendEquation() call.

The most common options for glBlendFunc() parameters (i.e., srcFactor and destFactor) are shown in the following table:

| glBlendFunc() parameter | resulting srcFactor or destFactor |
|---|---|
| GL_ZERO | (0,0,0,0) |
| GL_ONE | (1,1,1,1) |
| GL_SRC_COLOR | (R<sub>src</sub>, G<sub>src</sub>, B<sub>src</sub>, A<sub>src</sub>) |
| GL_ONE_MINUS_SRC_COLOR | (1,1,1,1) − (R<sub>src</sub>, G<sub>src</sub>, B<sub>src</sub>, A<sub>src</sub>) |
| GL_DST_COLOR | (R<sub>dest</sub>, G<sub>dest</sub>, B<sub>dest</sub>, A<sub>dest</sub>) |
| GL_ONE_MINUS_DST_COLOR | (1,1,1,1) − (R<sub>dest</sub>, G<sub>dest</sub>, B<sub>dest</sub>, A<sub>dest</sub>) |
| GL_SRC_ALPHA | (A<sub>src</sub>, A<sub>src</sub>, A<sub>src</sub>, A<sub>src</sub>) |
| GL_ONE_MINUS_SRC_ALPHA | (1,1,1,1) − (A<sub>src</sub>, A<sub>src</sub>, A<sub>src</sub>, A<sub>src</sub>) |
| GL_DST_ALPHA | (A<sub>dest</sub>, A<sub>dest</sub>, A<sub>dest</sub>, A<sub>dest</sub>) |
| GL_ONE_MINUS_DST_ALPHA | (1,1,1,1) − (A<sub>dest</sub>, A<sub>dest</sub>, A<sub>dest</sub>, A<sub>dest</sub>) |
| GL_CONSTANT_COLOR | (R<sub>blendColor</sub>, G<sub>blendColor</sub>, B<sub>blendColor</sub>, A<sub>blendColor</sub>) |
| GL_ONE_MINUS_CONSTANT_COLOR | (1,1,1,1) − (R<sub>blendColor</sub>, G<sub>blendColor</sub>, B<sub>blendColor</sub>, A<sub>blendColor</sub>) |