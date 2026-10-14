```
#   self.mosSpecialty = self.subClass(
    self.mosChoice)
#if self.mosSpecialty == "":
#   self.mos = self.mosSelection|self.
mosChoice|
#else:
#   self.mos = self.mosSelection|self.
mosChoice| +
#   " (" + self.mosSpecialty + ")"
return self.mos
```

```
def mosSkills(self, mosChoice):
"""Determine default skill levels based on
MOS."""
```

```
if self.mosChoice == 0: #Supply
    self.chosenSkills["Supply"] = 20
elif self.mosChoice == 1:   #Crew Chief
    self.chosenSkills["Mechanic"] = 20
elif self.mosChoice == 2:   #Infantry
    self.chosenSkills["Small Arms"] = 20
    self.chosenSkills["Armed Combat"] = 10
    self.chosenSkills["Unarmed Combat"] =
    10
    self.chosenSkills["Swimming"] = 10
elif self.mosChoice == 3:   #Medical
    self.chosenSkills["First Aid"] = 20
elif self.mosChoice == 4:   #Not a value
    pass
elif self.mosChoice == 5:   #Heavy Weapons
    self.chosenSkills["Heavy Weapons"] =
    20
    self.chosenSkills["Small Arms"] = 10
    self.chosenSkills["Armed Combat"] = 10
    self.chosenSkills["Unarmed Combat"] =
    10
elif self.mosChoice == 6:   #Scout/Sniper
    self.chosenSkills["Recon"] = 15
```