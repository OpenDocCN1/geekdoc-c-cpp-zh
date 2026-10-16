
worked on the one side; organizations showed Return on Investment (ROI). On the other side, PSP metrics were not popular and were resisted by teams. There were two sides to PSP metrics, the good and the bad. People wanted simpler solutions and pushed aside PSP metrics.

Automated metrics survived, which depend on tools, and people were asked just to use data not to collect data. That by itself made a huge difference. The drawback is that nobody is motivated to use data collected by tools. A seeming gain became a loss. Such data did not connect well with people except in the form of reports and business intelligence; the intended recipients were senior managers and customers. Designers and testers did not care.

Simple core metrics were good and they worked. Fancy special metrics did not. Metrics planned and metrics used were worlds apart. At least metrics helped in goal setting. Process control loops using metrics were too circuitous and operated with time lags that by the time reports came projects were finished. Even the core metrics did not reach teams in time. The feedback loop disappeared on the way. Care was taken to install a metric, but no one thought about human communication.

![](img/2f042205c6c0e14747f198ed8f9c9f40_152_0.png)

> Without communication links with people, metrics fail.

## Metrics for Agile: Humanization

Agile projects have put people before processes and humanized metrics. Agile metrics instantly reach people through displayed charts and daily meetings. Metrics themselves are kept light, user-friendly, and direct. Code complexity is measured as high, medium, or low instead of using the sophisticated McCabe complexity number. Software sizes come in story points; one does not have to count function points using time-consuming rules by the International Function Point Users Group. More than that, metrics are readily used. Graphical elements have become signifiers instead of numerical indicators, where possible. The burn-down chart has replaced several metrics at once. Agile metrics influence day to day decision making.

## The Price of Humanization

Agile metric data are mostly in the ordinal scale (like in “high–medium–low” judgments). Ordinal data can be collected quickly without hassle. Ordinal data also have a degree of calculated approximation. The contrast is between precise but less used classic metric data versus approximate but humanized agile data. Working with a lower scale suffers information loss, a price we pay for humanization. However, that loss does not make agile metrics less scientific than classic metrics, if users are aware of the degree of approximation.

> The aim of science is not to open the door to infinite wisdom, but to set a limit to infinite error.
> 
> **Bertolt Brecht**
> *Life of Galileo*

> Sometimes a clearly defined error is the only way to discover the truth.
> 
> **Benjamin Wiker**
> *The Mystery of the Periodic Table*

## Common Agile Metrics

### Velocity

Agile velocity is story points delivered per sprint. This is the rate at which the team delivers tested features. To obtain the best out of this metric, sprints (or iterations) must be of consistent length.

### Story Point

This is an agile metric of software size, an agile counterpart of the classic function point. Story point is a numerical expression of textual metrics of size: very small, small, medium, large, very large, and so on. Because human judgment is in a non-linear scale, we prefer a nonlinear order of numbers: 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233,..., the Fibonacci series. In the Fibonacci scale, the following conversion table can be used to express software size.

| Software Size | Story Point |
|---|---|
| Very low | 1 |
| Low | 2 |
| Medium | 3 |
| Large | 5 |
| Very large | 8 |
| Extremely large | 13 |
| Next level | 21 |

Software requirements are broken into small features called *user stories*. The story point scale is used to judge the size of “user stories.”

![](img/2f042205c6c0e14747f198ed8f9c9f40_154_0.png)

> *User stories are analogous to the classical use cases.*
> *Story Points are analogous to Use Case Points.*

### Technical Debt

Number of defects discovered per iteration.

### Tests

The number of tests that have been developed, executed, and passed to validate a story.

### Level of Automation

The percentage of tests automated.

### Earned Business Value (EBV)

Business value attached to stories delivered. According to Dave Nicolette, “EBV may be measured in terms of hard financial value based on the anticipated return on investment (ROI) prorated to each feature or user story.”

### Burn-Down Chart

Burn-down represents the remaining work of the project versus the remaining human resources. This information can be presented every week until a complete release. Burn-down chart is a famous agile visual used to track progress. Figure 9.1 shows an example of a burn-down chart.

A common practice is to plot a burn-down chart for every team and for each iteration. This provides the necessary biofeedback to teams to control backlog and to attain iteration goals in time.

### Burn-Up Chart

Burn up represents work finished. Figure 9.2 illustrates a burn-up chart (BUC).

The y-axis is a cumulative plot of stories developed iteration by iteration. The ideal performance line is plotted along the actual performance line to provide guidance and to measure performance gaps. The BUC can be used when several stories are developed concurrently. This is a chart of stories built and work done; this records achievement and not merely activities.

![](img/2f042205c6c0e14747f198ed8f9c9f40_155_0.png)

Figure 9.1 Burn-down chart.

![](img/2f042205c6c0e14747f198ed8f9c9f40_155_1.png)

Figure 9.2 Burn-up chart.

### Burn Up with Scope Line

A BUC with scope line marked above as shown in Figure 9.3 has an advantage. Changing scope can be portrayed in this form and is not so easy in the other two charts.

![](img/2f042205c6c0e14747f198ed8f9c9f40_156_0.png)

Figure 9.3 Burn-up chart with scope line.

## BOX 9.3 A REBIRTH

Many classic metrics are reborn into the agile world with new names. Productivity used to be measured as KLOC/man month. This metric is called velocity and measured as story points delivered per iteration. The basic concept remains the same, but the metrics used in the calculation are now less precise but more convenient. The expectations have shifted. Velocity metric is not used as a target, and that seems to have made all the difference; the metric has received social acceptance.

> When a measure becomes a target it ceases to be a good measure.
> 
> Goodhart's Law

Good old defects are now called technical debt. For long, programmers knew that there should be no stigma attached to software defects. The new definition upholds a dignity and the human spirit.

## Adding More Agile Metrics

The present metric system is a victim of poor implementation. It is overdesigned but underutilized. Agile metrics are simple and easy to implement; they have to be simple to honor the very spirit of agile methodology.

Hartmann and Dymond [1] list 10 attributes of a typical agile metric system as follows:

- 1. It affirms and reinforces lean and agile principles.
- 2. It follows trends, not numbers. Measure “one level up” to ensure you measure aggregated information, not suboptimized parts of a whole.
- 3. It belongs to a small set of metrics and diagnostics. A “just enough” metrics approach is recommended: too much information can obscure important trends.
- 4. It measures outcome, not output.
- 5. It is easy to collect.
- 6. It reveals rather than conceals.
- 7. It provides fuel for meaningful conversation.
- 8. It provides feedback on a frequent and regular basis.
- 9. It measures value.
- 10. It encourages “good enough” quality.

It may be noted that the above attributes can be applied to metrics in conventional life cycles too.

Hartmann and Dymond conclude that the key agile metric should be business value, and they note,

> Agile methods encourage businesses to be accountable for the investment in software development efforts. In the same spirit, the key metrics we use should allow us to measure this accountability. Metrics should help validate businesses that make smart software investments and teams that deliver business value quickly.

ROI begins with the first release of feature. Value must be measured. Delivering value early is the hallmark of agile projects.

However, in extreme programming, project teams have added metrics that are not so simple. Teams use the following metrics where refactoring takes place at the end of each iteration source code:

- 1. Coupling
- 2. Cyclomatic complexity
