```
(retract; 'Gatewood-deJonge1995)

(inquire Vega-parallax-distance
(vega-parallax-distance)
(has-value (interval 7.663 7.7))
(depends-on fvanleeuwen2007nov
gatewood2008
bohlinggillillilland2004))
```

Indeed it does. The 1995 measurement pulled in the high end of the interval.

# Measurements Improved!

We have two ways of computing the distance to Vega–from parallax and from magnitude. There is something remarkable: the parallax and magnitude measurement intervals are each improved using the information coming from the other. This is required in order for the system to be consistent.

Look at the apparent magnitude of Vega. The original measurement supplied from Bohlin and Gilliland was m = 0.026 ± 0.008. This translates to the interval

```
-->interval 0.026 0.008
(interval .018 .034)
```

But now the value is a bit better—[0.018, 0.028456]:

```
(inquire Vega-apparent-magnitude
(vega-apparent-magnitude)
(has-value (interval 1.8e-2 2.8456e-2))
(depends-on fvanleeuwen2007nov
bohlin-gilliland2004))
```

The high end had to be pulled to be consistent with the information from the parallax measurements. This is true for each measurable quantity. The absolute magnitude supplied by Gatewood 2008 (page 338) was:

```
-->interval 0.582 0.014
(interval .568 .596)
```

But now the low end is pulled in: