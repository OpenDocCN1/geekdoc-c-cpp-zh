of the data. The procedure mas->radians converts milliarcseconds to radians. The procedure +->interval makes an interval centered on its first argument:

```
(define (+->interval value delta)
(make-interval (n-: value delta) (n+: value delta)))
```

# So the Vega-parallax cell is given the interval

```
(+->interval (mas->radians 125) (mas->radians 50))
(interval 3.636120683215196-7 8.48423941941688e-7)
```

Struve's estimate of the error in his result was a pretty big fraction of estimated parallax. His estimate for the distance to Vega is pretty rough (5.7 to 13.3 or 9.5 ± 3.8 parcels):

```
(get-value-in Vega-parallax-distance)
(interval 5.7142857143291135 13.3333333334721)
```

```
(interval +-> (get-value-in Vega-parallax-distance)
(+- 9.52380952388316 3.8095238095540473)
```

This interval value is supported by the premise FGWvonStruve1837.

```
(get-premises Vega-parallax-distance)
(support-set fgwvonstruve1837)
```

We use a procedure inquire that nicely shows the value of the cell and the support for that value:3

```
(inquire Vega-parallax-distance)
((vega-parallax-distance)
(has-value interval 5.7143e0 1.3333e1)
(depends-on fgwvonstruve1837)
(because
(p/: c* c:parallax<->distance)
(au 4.8481e-6)
(t 3.6361e-7 8.4842e-7)))
```

A tight bound, reported by Russell et. in 1982 [106], is

```
(tell! Vega-parallax
(+->interval (mas->radians 124.3) (mas->radians 4.9))
'JRussell-etal-1982)
```