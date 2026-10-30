# Nearest rank percentile

To find the nearest rank in the list of ticket durations provided earlier in this section, you would use the following formula:

$$n = (r / 100) * N$$

Plugging your values into the formula gives you the following result:

$$n = 95/100 * 20$$

$$n = 19/20 * 20$$

$$n = 19$$

Therefore, the 19th number in the sorted list is your 95th percentile. This results in an estimate of 10 days. Note that this method says nothing about the magnitude of possible overrun if your estimate is wrong. Whether that 20th number was 18 or 180, the long-tail value is ignored in this calculation, so even adding a confidence interval does not give the full picture.

> **Tip** The sample interval here is relatively low. If you can deliver an average of only four tickets per week, it would take five weeks to get a sample size large enough to calculate the 95th percentile.

Now that you can give a more accurate estimate of the time that a ticket might take, you can attach an SLA to your classes of service. For each ticket type, the SLA can state a different 95th percentile estimate for completion.

In the case of defect tickets, a shorter cycle time—and therefore a better SLA—can be given. This highlights the importance of fixing defects over normal feature-delivery work.

Similarly, dedicated refactor or redesign tickets can take longer than standard feature-delivery work. This allows for a longer cycle time and a shorter SLA.

In summary, by separating classes of service, it is possible to treat various work streams differently. This removes what would be outliers if you were to group together work items. SLAs can be attached to classes of service, rather than to the team’s work as a whole.

# Class WIP limits

Another advantage of separate classes of service is the ability to specify work-in-progress (WIP) limits for each category rather than for any work that arrives in a column.

This is useful when you have some types of work that you want to ensure make some progress without stalling and without dominating the team’s time. The best example of this is refactor work. For the uninitiated, refactoring is covered in further detail in Chapter 6, “Refactoring.”