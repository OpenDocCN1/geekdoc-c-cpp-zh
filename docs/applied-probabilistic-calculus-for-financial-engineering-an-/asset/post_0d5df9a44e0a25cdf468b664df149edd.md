
| Parameter | Description |
|---|---|
| line.type | type of line in line chart |
| bar.type | type of barchart - ohlc or hlc |
| theme | a chart.theme object |
| layout | if NULL bypass internal layout |
| major.ticks | where should major ticks be drawn |
| minor.ticks | should minor ticks be drawn? |
| yrange | override y-scale |
| plot | should plot be drawn |
| up.col | up bar/candle color |
| dn.col | down bar/candle color |
| color.vol | color code volume? |
| multi.col | 4 color candle pattern |
| ... | additional parameters |

## Details

Currently, charts display standard style OHLC charts familiar in financial applications or line charts not passing OHLC data. Works with objects having explicit time-series properties.

Line charts are created with close data, or from single column time series. The subset argument can be used to specify a particular area of the series to view. The underlying series is left intact to allow for TA functions to use the full data set. Additionally, it is possible to use syntax borrowed from the first and last functions, for example, "last 4 months."

TA allows for the inclusion of a variety of chart overlays and technical indicators. A full list is available from addTA. The default TA argument is addVo() - which adds volume, if available, to the chart being drawn. theme requires an object of class chart.theme, created by a call to chartTheme. This function can be used to modify the look of the resulting chart. See chart.theme for details. line.type and bar.type allow further fine tuning of chart styles to user tastes. multi.col implements a color coding scheme used in some charting applications, and follows the following rules:

- grey => Op[t] < Cl[t] and Op[t] < Cl[t-1]
- white => Op[t] < Cl[t] and Op[t] > Cl[t-1]
- red => Op[t] > Cl[t] and Op[t] < Cl[t-1]
- black => Op[t] > Cl[t] and Op[t] > Cl[t-1]

reChart takes any number of arguments from the original chart call and redraws the chart with the updated parameters. One item of note: If multiple color bars/candles are desired, it is necessary to respecify the theme argument.

Additionally, it is not possible to change TA parameters at present.

This must be done with `addTA`/`dropTA`/`swapTA`/`moveTA` commands.

## Value

Returns a standard chart plus volume, if available, suitably scaled.

If `plot=FALSE`, a chob object will be returned.

## Note

Most details can be fine-tuned within the function, though the code does a reasonable job of scaling and labeling axes for the user.

The current implementation maintains a record of actions carried out for any particular chart. This is used to recreate the original when adding new indicator.

A list of applied TA actions is available with a call to `listTA`.

This list can be assigned to a variable and used in new chart calls to recreate a set of technical indicators. It is also possible to force all future charts to use the same indicators by calling `setTA`.

Additional motivation to add outlined candles to allow for scaling and advanced color coding is owed to Josh Ulrich, as are the base functions (from TTR) for the yet to be released technical analysis charting code.

Many improvements in the current version were the result of conversations with Gabor Grothendieck. Many thanks to him.

## Author(s)

Jeffrey A. Ryan

## References

Josh Ulrich - TTR package and multi.col coding

## See Also

`getSymbols`, `addTA`, `setTA`, `chartTheme`

## Examples

```
## Not run:
getSymbols("YHOO")
chartSeries(YHOO)
chartSeries(YHOO, subset='last 4 months')
chartSeries(YHOO, subset='2007::2008-01')
chartSeries(YHOO, theme=chartTheme('white'))
chartSeries(YHOO, TA=NULL) # no volume
chartSeries(YHOO, TA=c(addVo(),addBBands()))
#add volume and Bollinger Bands from TTR
addMACD() # add MACD indicator to current chart
setTA()
chartSeries(YHOO)
#draws chart again, this time will all indicators present
## End(Not run)
```

```
> chartSeries(YHOO)
> chartSeries(YHOO,
    subset='last 4 months')
> # Outputting: Figure 4.22
```

![](img/551ca8853d2ba8528201e7a57e5006b4_383_0.png)

Figure 4.22

```
> chartSeries(YHOO, subset='last 4 months')
> chartSeries(YHOO,
    subset='2007::2008-01')
> # Outputting: Figure 4.23
> 
> chartSeries(YHOO, subset='2007::2008-01')
```

![](img/551ca8853d2ba8528201e7a57e5006b4_383_1.png)

Figure 4.23

```
> chartSeries(YHOO,theme=chartTheme
('white'))
```

```
> # Outputting: Figure 4.24
```

![](img/551ca8853d2ba8528201e7a57e5006b4_384_0.png)

Figure 4.24

```
> chartSeries(YHOO,theme=chartTheme
('white'))
```

```
> chartSeries(YHOO,TA=NULL) #no volume
```

```
> # Outputting: Figure 4.25
```

![](img/551ca8853d2ba8528201e7a57e5006b4_384_1.png)

Figure 4.25

```
> chartSeries(YHOO, TA=NULL)  #no volume
> chartSeries(YHOO, TA=c(addVo(),
  addBBands()))
#add volume and Bollinger
> # Outputting: Figure 4.26
```

![](img/551ca8853d2ba8528201e7a57e5006b4_385_0.png)

Figure 4.26

```
> chartSeries (YHOO, TA=c(addVo(),
+               addBBands()))
>   # add volume and Bollinger
> addMACD() # add MACD indicator to
+   # current chart
> # Outputting: Figure 4.27
> addMACD() # add MACD indicator to
+   current chart
> setTA()
> # Outputting: Figure 4.28
> setTA()
> chartSeries(YHOO) # draws chart again,
+   # this time will all indicators present
```

![](img/551ca8853d2ba8528201e7a57e5006b4_386_0.png)

Figure 4.27

![](img/551ca8853d2ba8528201e7a57e5006b4_386_1.png)

Figure 4.28

![](img/551ca8853d2ba8528201e7a57e5006b4_387_0.png)

Figure 4.29

```
> # Outputting: Figure 4.29
> 
> chartSeries(YHOO)
+ # draws chart again, this time
+ # with all indicators present
> ```
```

## Review Questions for Section 4.5

- 1. Define: univariate, bivariate, and multivariate data analyses, giving an example of each.

- 2. a How are these analyses carried out in the R environment?
  b Give examples of the R code segments for these analyses.

- 3. a What is meant by regression analysis?
  b How is regression analysis used in data analysis?

- 4. a How is regression analysis carried in the R environment?
  b Provide examples of the R functions used for regression analysis.

- 5. a Summarize the two uses of the ANOVA Table in data analysis.
  b For data analysis, suggest an applicable R code segments.

shy away from risky assets when valuations are most attractive and when traditional portfolio theory would predict greater demand for equities to rebalance a portfolio. This effect is especially noteworthy given the increasing use of risk tolerance questionnaires (RTQs) by advisors when recommending an optimal client portfolio allocation. This is significant because the primary reason that individual investors underperform institutional investors is their *tendency to sell equity mutual funds during a bear market!*

Sophisticated investors, such as those who use index (versus active) mutual funds and buy institutional share classes (i.e., have more wealth and, therefore, more implied investing human capital), exhibit lower time-varying risk aversion. It is also noted that a consistent negative relation between time-varying risk aversion and net equity mutual fund flows may be established. Trail compensation, which provides the same incentive whether the client buys new funds to match their changing risk preferences, is associated with a lower variable risk preference bias.

## 5.2 Classical Assets Allocation Approaches

*Asset allocation* is the undertaking of an investment strategy in order to balance risk versus reward by adjusting the percentage of each asset in an investment portfolio according to the investor's risk tolerance, goals, and investment time frame.

Figure 5.1 is a typical asset allocation pie chart.

![](img/551ca8853d2ba8528201e7a57e5006b4_391_0.png)

Figure 5.1 An asset investment pie chart – with a diverse portfolio.
