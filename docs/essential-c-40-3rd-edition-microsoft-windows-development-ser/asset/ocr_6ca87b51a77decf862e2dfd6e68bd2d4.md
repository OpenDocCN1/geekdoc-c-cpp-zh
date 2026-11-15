```
{
    "Fabien Barthez", "Gregory Coupet",
    "Mickael Landreau", "Eric Abidal",
    "Jean-Alain Boumsong", "Pascal Chimbonda",
    "William Gallas", "Gael Givet",
    "Willy Sagnol", "Mikael Silvestre",
    "Lilian Thuram", "Vikas Dhorasoo",
    "Alou Diarra", "Claude Makelele",
    "Florent Malouda", "Patrick Vieira",
    "Zinedine Zidane", "Djibril Cisse",
    "Thierry Henry", "Franck Ribery",
    "Louis Saha", "David Trezeguet",
    "Sylvain Wiltord",
},
},
new
{
    TeamName = "Italy",
    Players = new string[]
    {
        "Gianluigi Buffon", "Angelo Peruzzi",
        "Marco Amelia", "Cristian Zaccardo",
        "Alessandro Nesta", "Gianluca Zambrotta",
        "Fabio Cannavaro", "Marco Materazzi",
        "Fabio Grosso", "Massimo Oddo",
        "Andrea Barzagli", "Andrea Pirlo",
        "Gennaro Gattuso", "Daniele De Rossi",
        "Mauro Camoranesi", "Simone Perrotta",
        "Simone Barone", "Luca Toni",
        "Alessandro Del Piero", "Francesco Totti",
        "Alberto Gilardino", "Filippo Inzaghi",
        "Vincenzo Iaquinta",
    }
}
}
});
```

```
IEnumerable<string> players =
    worldCup2006Finalists.SelectMany(
        team => team.Players);

Print(players);
```

```
// ...
```

The output from this listing has each player's name displayed on its own line in the order in which it appears in the code. The difference between Select() and SelectMany() is the fact that Select() would return two items, one corresponding to each item in the original collection.