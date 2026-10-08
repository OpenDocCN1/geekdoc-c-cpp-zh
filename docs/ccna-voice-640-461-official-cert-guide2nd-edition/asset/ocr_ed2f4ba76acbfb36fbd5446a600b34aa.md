![](bbox=[0.145, 0.078, 0.826, 0.415])

# ### Figure 6-15 Translating DID Ranges to Internal Extensions

The first step to configure the translation profiles is to create the translation rules. These use the general syntax shown in Example 6-20.

# ### Example 6-20 Translation Rule General Syntax

```
Router(config)# voice translation-rule rule number
Router(cfg-translation-rule)# rule 1 /match/ /set/
Router(cfg-translation-rule)# rule 2 /match/ /set/
Router(cfg-translation-rule)# rule 3 /match/ /set/ ... and so on
```

Example 6-21 configures the necessary translation rule for the scenario in Figure 6-15.

# ### Example 6-21 Configuring Translation Rules

```
HQ_ATR(config)# voice translation-rule 1
HQ_ATR(cfg-translation-rule)# rule 1 ?
/WORD/ Matching pattern
  reject Call block rule
HQ_ATR(cfg-translation-rule)# rule 1 /6/ ?
/WORD/ Replacement pattern
HQ_ATR(cfg-translation-rule)# rule 1 /6/ /5/
```

The syntax in rule 1 command may look a little cryptic. The first entry between the set of forward slashes (/) is the match statement. This tells the router, "Look for the number 6." The entry between the second set of forward slashes is the set statement. This tells the router, "Replace the 6 you found from the match statement with a 5." In this case, the router changes the first 6 that is found to be a 5.