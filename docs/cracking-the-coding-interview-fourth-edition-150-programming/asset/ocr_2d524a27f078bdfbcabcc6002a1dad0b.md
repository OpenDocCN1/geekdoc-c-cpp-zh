# Solutions to Chapter 12 | System Design and Memory Limits

```
public int getID() { return ID; }
public int getMachineID() { return machineID; }
public void addFriend(int id) { friends.add(id); }

// Look up a person given their ID and Machine ID
public Person lookupFriend(int machineID, int id) {
    for (Machine m : server.machines) {
        if (m.machineID == machineID) {
            for (Person p : m.persons) {
                if (p.ID == ID)
                    return p;
            }
        }
    }
    return null;
}

// Look up a machine given the machine ID
public Machine lookupMachine(int machineID) {
    for (Machine m : server.machines) {
        if (m.machineID == machineID)
            return m;
    }
    return null;
}

public Person(int ID, int machineID) {
    this.ID = ID;
    this.machineID = machineID;
}
```