```
self.mosSelection[16] = "Interrogator"
self.mosSelection[17] = "Intelligence:
Xenomorphs"
if self.intel >= 10 and self.dex >= 10 and
("O1" <= self.rank <= "O4"):
self.mosSelection[18] = "Pilot"
self.mosSelection[19] = "Co-Pilot/
Gunner"
###Tank and APC Commander MOS have the
same requirements as pilots
### but are added after the 'Armor'
MOS's.
self.mosSelection[13] = "Tank
Commander"
self.mosSelection[14] = "APC Commander"

def eligibleMOS(self):
"""Displays MOS's available to character.
"""

print "You are eligible for the following
MOS's:"
for key in self.mosSelection.keys():
print key, self.mosSelection[key]
self.mosChoice = int(raw_input("""\nPlease
choose the number of
the MOS you want: """))
self.mos = self.mosSelection[self.
mosChoice] #Rename selection
print "You chose the", self.mos,
"specialty."
###Subclasses removed for possible later
use
#if self.mosChoice == 2 or self.mosChoice
== 4 or self.mosChoice == 9 or
#
self.mosChoice == 10:
```