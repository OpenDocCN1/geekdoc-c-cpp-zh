Interestingly, CTA1 has been toppled from its premier position in the rankings by CTA3. In other words, CTA1 has been found guilty of free-riding on the market to a certain extent in order to produce a percentage of their returns. This is generally frowned upon in the industry since a manager should not get paid risk on an easily replicable asset class as the same exposure can usually be obtained cheaply using ETFs or futures held long and rolled as necessary. CTA3, which was ranked by the SR, is now in place first with a JA of 12.02%. While CTA1 is still in second place, GM1 keeps its place in with a similar ranking to the TR, LS1 has been demoted to fourth having been in the SR rankings. MN52 is still the better bounded fund.

# ### 5.5.4 M-Squared

The M-squared (MM) metric was developed by Modigliani and Modigliani¹³ as a risk-adjusted measure which could be more easily interpreted by an average investor once the various hedge funds had been volatility adjusted for their average returns and then ranked. The intuition is that by using a benchmark with an estimated volatility of the fund is either leveraged or de-leveraged so that its volatility matches that of the market benchmark. The leveraged or de-leveraged return of the fund is then reported and ranked. As such, the fund's return can be interpreted as the return that would have been produced the fund's volatility been equivalent to that of the market benchmark. When various funds are processed in this way and ranked, it is easier for the less sophisticated investor to see how they outperform the benchmark to which they have their risk profile matched. In our case, the market benchmark (SDX) has an analysed return of 5.36% and a volatility of 10.90% for matching purposes. MM is given by:

> $MM = \frac{\sigma_M}{\sigma_P}(R_p - R_F) - R_F \quad (5.18)$

Source 5.8: THE MM () member declaration — and definition.

| SOURCE 5.8: THE MM () MEMBER DECLARATION AND DEFINITION |
| --- |
| // |
| //Metrics.h |
| // ... |
| V1DD MM(V2DD& v, const DBL& r); // MM() |