```
`int[] test = new int[10];`
```

The example variable holds a reference to the memory apportioned by new. This memory is enormous enough to hold ten components of type int. For this situation, when test is first made, it alludes to no physical article. It is simply after the second articulation executes that example alludes to a cluster.

An individual component inside a cluster is gotten to by utilization of a record. A record portrays the situation of a component inside a cluster. In C#, all clusters have zero as the record of their first component. Since test has ten components, it has record estimations of 0 through 9. To record a cluster, indicate the quantity of the component you need, encompassed by square sections.

# ## Ref And Out Parameter:

As just clarified, as a matter of course, esteem types, for example, int or burn, are passed by an incentive to a technique. This implies changes to the parameter that gets a worth sort won't influence the genuine contention utilized in the call. You can, notwithstanding, modify this conduct. Using the ref and out watchwords, it is conceivable to pass any of the worth sorts by reference. Doing so permits a strategy to adjust the contention utilized in the call. Prior to going into the mechanics of utilizing ref and out, it is helpful to comprehend why you should pass a worth kind by reference. As a rule, there are two reasons: to permit a strategy to modify the substance of its contentions or to enable a technique to return mutiple esteem. We should take a gander at each reason in detail.

Frequently, you will need a technique to have the option to work on the real contentions that are passed to it. The quintessential case of this is a "swap" strategy that trades the estimations of its two contentions. Since worth sorts are passed by esteem, it is preposterous to expect to compose such a strategy that swaps the estimation of two ints, for instance, utilizing C#'s default call-by-esteem parameterpassing system. The ref modifier takes care of this issue.

As you probably are aware, an arrival articulation empowers a technique to restore an incentive to its guest. Be that as it may, a strategy can return just one worth each time