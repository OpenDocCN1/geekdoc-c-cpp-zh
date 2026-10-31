```
```r
[57] "meucci.moments"              "meucci.ranking"
[59] "minimax_objective"             "mult.portfolio.spec"
[61] "objective"                     "optimize.portfolio"
[63] "optimize.portfolio.parallel"   "optimize.portfolio.rebalancing"
[65] "optimize.portfolio.rebalancing_v1" "optimize.portfolio_v1"
[67] "optimize.portfolio_v2"         "portfolio.spec"
[69] "portfolio_risk_objective"      "pos_limit_fail"
[71] "position_limit_constraint"     "quadratic_utility_objective"
[73] "random_portfolios"             "random_portfolios_v1"
[75] "random_portfolios_v2"          "random_walk_portfolios"
[77] "randomize_portfolio"           "randomize_portfolio_v1"
[79] "randomize_portfolio_v2"        "regime.portfolios"
[81] "return_constraint"              "return_objective"
[83] "risk_budget_objective"          "rp_grid"
[85] "rp_sample"                      "rp_simplex"
[87] "rp_transform"                   "scatterFUN"
[89] "set.portfolio.moments"          "statistical.factor.model"
[91] "trailingFUN"                    "transaction_cost_constraint"
[93] "turnover"                       "turnover_constraint"
[95] "turnover_objective"             "update_constraint_v1tov2"
[97] "var.portfolio"                  "weight_constraint_objective"
[99] "weight_sum_constraint"
> ac.ranking
function (R, order, ...)
{
    if (length(order) != ncol(R))
        stop("The length of the order vector must equal the number of
assets")
    nassets <- ncol(R)
    if (hasArg(max.value)) {
        max.value <- match.call(expand.dots = TRUE)$max.value
    }
    else {
        max.value <- median(colMeans(R))
    }
    c_hat <- scale.range(centroid(nassets), max.value)
    out <- vector("numeric", nassets)
    out[rev(order)] <- c_hat
    return(out)
}
<environment: namespace:PortfolioAnalytics>
> data(edhec)
> edhec
```
```