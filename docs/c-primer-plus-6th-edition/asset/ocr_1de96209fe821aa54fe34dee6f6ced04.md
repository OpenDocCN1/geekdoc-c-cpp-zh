```
cerr << "Can't open " << file << " file for output:\n";
exit(EXIT_FAILURE);
}

cout << "Enter planet name (enter a blank line to quit):\n";
cin.get(pl.name, 20);
while (pl.name[0] != '\0')
{
	eatline();
	cout << "Enter planetary population: ";
	cin >> pl.population;
	cout << "Enter planet's acceleration of gravity: ";
	cin >> pl.g;
	eatline();
	fout.write((char *) &pl, sizeof pl);
	cout << "Enter planet name (enter a blank line "
		"to quit):\n";
	cin.get(pl.name, 20);
}
fout.close();

// show revised file
fin.clear();   // not required for some implementations, but won't hurt
fin.open(file, ios_base::in | ios_base::binary);
if (fin.is_open())
{
	cout << "Here are the new contents of the "
		<< file << " file:\n";
	while (fin.read((char *) &pl, sizeof pl))
	{
		cout << setw(20) << pl.name << ": "
			<< setprecision(0) << setw(12) << pl.population
			<< setprecision(2) << setw(6) << pl.g << endl;
	}
	fin.close();
}
cout << "Done.\n";
return 0;
}
```

Here is a sample initial run of the program in Listing 17.19:

```
Enter planet name (enter a blank line to quit):
Earth
Enter planetary population: 6928198253
Enter planet's acceleration of gravity: 9.81
```