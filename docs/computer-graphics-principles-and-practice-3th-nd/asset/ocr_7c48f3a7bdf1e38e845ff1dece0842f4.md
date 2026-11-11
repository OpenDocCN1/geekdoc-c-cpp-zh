```
```text
repeat N times:
  // Computed by the emitter
  L_i = ...
  M_i = L_i + max(-m.dot(w_i), 0.0f) * A / |L_p - Q|^2

  // Computed by the integrator (i.e., renderer)
  if there is an occluder on the line from P to Q then M_i = 0
  L_o += M_i * bsdf.evaluate(...) * n.dot(w_i) / N
```
```

Thus, one interpretation of the deprecated fixed-function OpenGL Phong shading and (to some degree) shading in WPF is that the light “intensities” correspond to the function \(M\), whose units are watts per square meter. This particular quantity is not one that has a standard name in radiometry, however, and we will not mention it again. It’s also worth noting that in most simple rendering using the classical model, the \(1/r^2\) falloff is not actually modeled, so the claim that what’s used as an intensity in \(M\) is somewhat suspect. What’s true is that if you wish to use the classical model to approximate physical reality, then you *should* use the \(1/r^2\) falloff, and you should assign luminaires “intensity” values computed according to the formula for \(M\).

# 14.11.3.4 Applying the Interface to Photon Emission

Algorithms such as bidirectional ray tracing and photon mapping track the path of virtual photons forward from the light source into the scene. These virtual photons differ from the real photons that they model in two respects. The first distinction is that their state includes a position, a direction of propagation, and the *power* of the photon. Real photons transport *energy*, but rendering considers steady-state light transport, so it tracks the rate of energy delivery. It is more accurate to say that each virtual photon models a stream of photons, or that it models a segment of a light-transport path. The second distinction from real photons is that trillions of real photons contribute to a single real image, whereas renderers typically sample only a few million virtual photons (although each represents a stream of photons, so in truth many more real photons are implicitly modeled).

The first step of photon tracing is to emit photons from the sources in the scene. Listing 14.12 shows how to use our light interface to sample numPhotons-emitted virtual photons with a probability density function proportional to the power of each light source.

*Listing 14.12: Generating `numPhotons` photons from a set of lights; for example, for photon mapping.*

```
```cpp
void emitPhotons
(const int                  numPhotons,
 const Array<Light*>&       lightArray,
 Array<Photon>&             photonArray) {

  const Power& totalPower;
  for (int i = 0; i < lightArray.size(); ++i)
    totalPower += lightArray[i]->power();

  for (int p = 0; p < numPhotons; ++p) {
    // Select light with probability L.power.sum()/totalPower.sum()
    const Light* light = chooseLight(lightArray, totalPower);

    Point3        Q;
    Vector3       w_o;
```
```