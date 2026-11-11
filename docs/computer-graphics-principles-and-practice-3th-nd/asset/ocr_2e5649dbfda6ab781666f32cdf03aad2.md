# Table 32.1: Symbols used in the path tracer.

| Symbol | Meaning |
|---|---|
| E | The eye point. |
| P | A surface point in the scene, often the first one encountered by a ray from the eye, but sometimes used generically. |
| Q, Q_j | A point on the surface of a luminaire or some other source of light arriving at P, such as an illuminated reflective surface. |
| n_P, n_Q | The unit normal vector at P, which we’ve denoted n(P) previously, or the same thing for Q. |
| ω_i | A unit vector pointing from P toward some source of light. |
| ω_o | A unit vector pointing from P in the direction in which reflected light from ω_i exits, typically toward E. |
| ω | A generic name for a unit vector, typically based at P. |
| L(P, ω) | The radiance at a surface point P in direction ω. Note that in this chapter we only define L for surface points. |
| L^e(P, ω) | The light emitted at point P in direction ω; zero except when P is a point of a luminaire. |
| L_j^e(P, ω) | The light emitted by the jth luminaire. |
| L^t(P, ω) | The light reflected or transmitted (refracted) at P in direction ω. L = L^e + L^t. |
| L^ref(P, ω) | The light reflected at P in direction ω. |
| L^trans(P, ω) | The light transmitted at P in direction ω. L^t = L^ref + L^trans. |
| f_s | The bidirectional scattering distribution function. |
| f_s^∞ | The “impulse” part of f_s, corresponding to transmission or mirror reflection. |
| f_s^0 | The finite part of f_s, corresponding to nonmirror reflection. |

Let’s suppose that there are k luminaires in the scene, each producing an emitted radiance field (Q, ω) ↦ L_j^e(Q, ω), j = 1,...,k which for any point-vector pair (Q, ω) with Q on a surface and ω · n_Q > 0 is zero, except for points on the jth luminaire, and directions ω in which the light emits radiance. Most often this radiance field will be Lambertian, that is, L_j^e(Q, ω) will be a constant for Q on the luminaire and any ω with ω · n_Q > 0; it’s zero otherwise. But for now, we’ll just assume that it’s a general light field.

Furthermore, let’s assume that all surfaces are opaque—the only scattering that takes place is reflection. The change to include transmission will be relatively minor.

The rendering equation tells us that if P is the first point at which the ray t ↦ E − tω hits the geometry in the scene (see Figure 32.7), then

L(E, ω) = L(P, ω)    (32.5)

= L^e(P, ω)（emitted） + ∫_{ω_o∈S²(n_P)} f_s(P, ω_o, ω) L(P, −ω_o) |ω_i · n_P| dω_i（scattered）.    (32.6)

![](bbox=[0.704, 0.613, 0.931, 0.889])