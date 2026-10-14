```
```
return self.rank
```

```
#-----Get MOS
```

```python
def requirements(self):
    """Adds eligible MOS's to selection
    dictionary.

    Takes various character attributes and
    determines if additional MOS choices
    are available."""

    if self.intel >= 11:
        self.mosSelection[3] = "Medical"
    ###Value "4" is missing due to changing
    positions
    if self.str >= 12:
        self.mosSelection[5] = "Heavy Weapons"
    if (self.dex + self.intel + self.will) >= 
        40:
        if multiDie(1,3) >= 85:
            self.mosSelection[6] = "Scout/
            Sniper"
    if (self.str + self.dex + self.intel +
        self.will) >= 50:
        if multiDie(1,3) >= 85:
            self.mosSelection[7] = "Recon"
    if self.str >= 10 and self.intel >= 10:
        self.mosSelection[8] = "Combat
            Engineer"
    if self.dex >= 11:  #Armor MOS's
        self.mosSelection[9] = "Tank Driver"
        self.mosSelection[10] = "Tank Gunner"
        self.mosSelection[11] = "APC Driver"
        self.mosSelection[12] = "APC Gunner"
    if self.intel + self.will >= 27:   #
        Intelligence MOS's
        self.mosSelection[15] = "Intelligence
            Analyst"
```
```