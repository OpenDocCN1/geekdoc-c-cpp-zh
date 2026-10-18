```
```cpp
/* March ray through volume and probabilistically shade sample point */
inline Vec3f marchRay(...)
{
    if (!intersect(volume->bounds, ray))
    {
        color[0] += 1.f;
        color[1] += 1.f;
        color[2] += 1.f;
    }
    else
    {
        const float texit = min(ray.tfar, image->dbuffer[pid]);
        const float offset = frandom(&rngs)*tstep;
        const float random = frandom(&rngs);

        float t = ray.tnear + offset;
        float d = 0.0f;
        while (t < t exit)
        {
            const float<3> point = ray.org + t*ray.dir;
            const float value = sampleVolume(volume, point)*volume->imax;

            d += value;

            if (random < d*iscale)
            {
                float<3> toLight = l - point;
                Normalize(toLight);

                const RGB scolor = { 0.f, d, d };

                RGB result = Ka*acolor*scolor;

                float<3> N =
                {
                    camera->eye[0] - point[0],
                    camera->eye[1] - point[1],
                    camera->eye[2] - point[2],
                };

                Normalize(N);

                color += (Ka*acolor + Kd*max(0.f, Dot(N, toLight))*color)*scolor;

                break;
            }

            t += tstep;
        }

        if (t > t exit)
        {
            color[0] += image->fbuffer[pid][0];
            color[1] += image->fbuffer[pid][1];
            color[2] += image->fbuffer[pid][2];
        }
    }

    return color;
}
```
```

# FIGURE 12.13

Rendering volume data as a participating medium with ispc. This cleanly vectorized ispc code implements a probabilistic approach to rendering volume data as a participating medium. Importantly, the code is easy to read, easy to maintain, ISA-portable, and highly performant. (Function interfaces omitted for brevity. Code snippet adapted from visbench/traceVolume.ispc:258–310.)