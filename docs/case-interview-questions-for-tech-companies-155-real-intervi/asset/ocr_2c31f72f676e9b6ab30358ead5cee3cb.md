# Answer

CANDIDATE: Is this during regular hours, rush hours or some inactive hours like 4AM?

INTERVIEWER: This is at 10AM.

CANDIDATE: What day is this?

INTERVIEWER: Monday.

CANDIDATE: Do you want to know how many cars I need on the road for this one hour, this day or this week? What mean, should I take into account the whole day, the whole week or just this one hour?

INTERVIEWER: You should take the whole week into account.

CANDIDATE: I can estimate how many cars I need, but I do want to point out since Uber drivers are not obligated to show up, usually take account rush hours and weekdays vs. weekends. What can we do increase their rates to incentivize them to show up, but it's not a 100% guarantee.

INTERVIEWER: That's fine.

CANDIDATE: Okay, I would make some assumptions:

+   * Rush hour is morning (7-9AM), lunch (12-1PM), and dinner (5-7PM) during the weekdays.
* Weekend rush hour would include late-night (12-2AM).
* Rush hour would probably see a 100% increase in traffic.
* Weekend would probably see an increase in traffic of 50%.

Let's plug all of this into a formula:

# Calculating cars for the week

```
Weekday Cars = Normal Hours * People per Hour * (1 + \frac{Rush Hours}{Hours per Day})
Weekday Cars = 19 * 1,000 * (1 + \frac{5}{24})
Weekday Cars = ~23,000
```

# Calculating cars for the weekend

```
Weekend Cars = Normal Hours * People per Hour * Weekend Bonus * (1 + \frac{Rush Hours}{Hours per Day})
Weekend Cars = 17 * 1,000 * 2 * (1 + \frac{7}{24})
Weekend Cars = ~44,000
```