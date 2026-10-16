```
new Team("Lotus", 1963, 1965, 1968, 1970, 1972, 1973, 1978),
    new Team("Brabham", 1966, 1967),
    new Team("Matra", 1969),
    new Team("Tyrrell", 1971),
    new Team("McLaren", 1974, 1984, 1985, 1988, 1989, 1990, 1991, 1998),
    new Team("Williams", 1980, 1981, 1986, 1987, 1992, 1993, 1994, 1996, 1997),
    new Team("Benetton", 1995),
    new Team("Renault", 2005, 2006),
    new Team("Brawn GP", 2009),
    new Team("Red Bull Racing", 2010, 2011, 2012, 1013),
    new Team("Mercedes", 2014, 2015)
};
}
return _teams;
}
```

# LINQ Query

Using these prepared lists and entities, you can do a LINQ query—for example, a query to get all world champions from Brazil sorted by the highest number of wins. To accomplish this you could use methods of the List<T> class—for example, the FindAll and Sort methods.
However, using LINQ there’s a simpler syntax as soon as you get used to it (code file LINQIntro/Program.cs):

```
private static void LinqQuery()
{
    var query = from r in Formula1.GetChampions()
                where r.Country =="Brazil"
                orderby r.Wins descending
                select r;

    foreach (Racer r in query)
    {
        WriteLine($"{r:A}");
    }
}
```

The result of this query shows world champions from Brazil ordered by number of wins:

```
Ayrton Senna, Brazil; starts: 161, wins: 41
Nelson Piquet, Brazil; starts: 204, wins: 23
Emerson Fittipaldi, Brazil; starts: 143, wins: 14
```

# The expression

```
from r in Formula1.GetChampions()
where r.Country =="Brazil"
orderby r.Wins descending
select r;
```

is a LINQ query. The clauses from, where, orderby, descending, and select are predefined keywords in this query.

The query expression must begin with a from clause and end with a select or group clause. In between you can optionally use where,