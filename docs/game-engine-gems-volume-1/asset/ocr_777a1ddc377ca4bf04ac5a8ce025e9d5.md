```
O /= Denom;
I *= (1.0 - O) / sampleCount;
return float4(I, O);
}
```

Then the enumerator and denominator of the ambient occlusion formula and the irradiance are computed in variables O, Denom, and I in the loop executed sampleCount times. A single occluder sample o is generated from prepared 2D points uniformly distributed in the unit disk (AO_RAND[k]). The depth map is fetched using the direction of the occluder, which results in occluder depth zstar. This depth is compared to the entry depth of the sphere zmin, exit depth zexit, and that of the intersection with the tangent plane zplane, determining the zmin-zmax interval where the function h is evaluated. In parallel, another interval is computed in Denom that describes the unoccluded case. This integral will be used for error compensation. Note that we also check whether the occluder is much closer to the eye than the shaded point and ignore such occlusions, which would otherwise result in false silhouette edges. If near occlusion happens and, according to the occluder's surface orientation, it can illuminate the shaded point, then the occluder's color is inserted into the average color used for indirect illumination. This fragment shader returns with the average indirect illumination and the ambient occlusion of the fragment, which is then composited with the previously calculated direct illumination result.

As the compiler unrolls loops that contain tex2D calls, we may run out of registers when the sample number is high (it is greater than 12 in the specified hardware). If more samples are needed, the tex2D calls should by replaced by tex2Dlod, which does not force loop unrolling. Surprisingly, this replacement does not degrade the performance.