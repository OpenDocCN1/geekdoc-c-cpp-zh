```
elif self.mosChoice == 13 or self.\
mosChoice == 14: #Vehicle Commanders
self.chosenSkills["Navigation"] = 15
self.chosenSkills["Tracked Vehicles"]
= 10
self.chosenSkills["Wheeled Vehicles"]
= 10
self.chosenSkills["Vehicle Weapons"] =
10
self.chosenSkills["Indirect Fire"] =
10
self.chosenSkills["Forward Observer"]
= 10
elif self.mosChoice == 15: #Analyst
self.chosenSkills["Electronics"] = 20
self.chosenSkills["Computers"] = 20
elif self.mosChoice == 16: #Interrogation
self.chosenSkills["Electronics"] = 10
self.chosenSkills["Computers"] = 10
self.chosenSkills["Interrogation"] =
20
elif self.mosChoice == 17: #Xenomorphs
self.chosenSkills["Electronics"] = 10
self.chosenSkills["Computers"] = 10
self.chosenSkills["Xenomorphs"] = 20
self.chosenSkills["Biology"] = 10
self.chosenSkills["Chemistry"] = 10
elif self.mosChoice == 18: #Pilot
self.chosenSkills["Aircraft"] = 20
self.chosenSkills["Vehicl Weapons"] =
10
elif self.mosChoice == 19: #Co-Pilot/
Gunner
self.chosenSkills["Aircraft"] = 10
self.chosenSkills["Vehicle Weapons"] =
20
else: print "**Invalid option**" #
Shouldn't reach
```