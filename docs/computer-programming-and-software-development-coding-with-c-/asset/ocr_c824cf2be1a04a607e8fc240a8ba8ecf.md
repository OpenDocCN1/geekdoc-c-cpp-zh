```
In [12]: for i, cluster in enumerate(model.means_):
    print(f"Group {i}")
    for j, col in enumerate(X.columns):
        print(f"{col} (mean): {round(cluster[j], 2)}")
    print("")
```

Group 0
Age (mean): 0.45
Occupation (mean): 4.04
Gender (mean): 0.61
Same_ofiice_home_location (mean): 0.33
kids (mean): 0.17
RM_save_money (mean): 0.75
RM_quality_time (mean): 0.4
RM_better_sleep (mean): 0.32
calmer_stressed (mean): 0.68
RM_professional_growth (mean): 3.51
RM_lazy (mean): 3.56
RM_productive (mean): 3.54
digital_connect_sufficient (mean): 0.38
RM_better_work_life_balance (mean): 2.25
RM_improved_skillset (mean): 3.31
RM_job_opportunities (mean): 0.24
Target (mean): 0.25

And again, I could perform a profile analysis to understand why someone is in one group or another. For example, a group with kids is more likely to want to work from home.