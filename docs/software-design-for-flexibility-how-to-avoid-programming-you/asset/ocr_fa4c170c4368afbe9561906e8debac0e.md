```
(c:magnitudes<->distance Vega-apparent-magnitude
Vega-absolute-magnitude
Vega-magnitude-distance)
```

We now provide some measurements. Vega is very bright; its apparent magnitude is very close to zero. (The Hubble space telescope was used to make this very precise measurement. Bohlin and Gillilland [14]).

```
(tell! Vega-apparent-magnitude
(->interval 0.026 0.008
'Bohlin-Gillilland2004)
```

And the absolute magnitude of Vega is also known to rather high precision [44]:

```
(tell! Vega-absolute-magnitude
(->interval 0.582 0.014
'Gatewood2008)
```

As a consequence we get a pretty nice estimate of the distance to Vega, which depends only on these measurements:

```
(inquire Vega-magnitude-distance
((vega-magnitude-distance)
(has-value interval 7.663 7.8199)
(depends-on gatewood2008 bohlingillilland2004))
```

Unfortunately, we have the distance in two different cells, let's connect them with a propagator:

```
(c:same Vega-magnitude-distance Vega-parallax-distance)
```

At this point we have an even better value for the distance to Vega—an interval whose high end is the same as before (on page 336), whose low end is a bit higher:

```
(inquire Vega-parallax-distance
((vega-parallax-distance)
(has-value interval 7.663 7.6787))
(depends-on fvanleeuwen2007 gatewood-dejonge1995
gatewood2008 bohlingillilland2004))
```

Does the 1995 measurement of Gatewood and de Jonge really matter here? Let's find out: