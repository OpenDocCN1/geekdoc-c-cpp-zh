```
QDataStream &operator<<(QDataStream &out, const Painting &painting)
    out << painting.title() << painting.artist()
    << quint32(painting.year());
    return out;
}
```

To output a Painting, we simply output two QStrings and quint32. At the end of the function, we return the stream. This is a common C++ idiom that allows us to use a chain of << operators with an output stream. For example:

```
out << painting1 << painting2 << painting3;
```

The implementation of operator>>() is similar to that of operator<<():

```
QDataStream &operator>>(QDataStream &in, Painting &painting)
    QString title;
    QString artist;
    quint32 year;

    in >> title >> artist >> year;
    painting = Painting(title, artist, year);
    return in;
```

There are several benefits to providing streaming operators for custom data types. One of them is that it allows us to stream containers that use the custom type. For example:

```
QList<Painting> paintings = ...;
out << paintings;
```

```
QList<Painting> paintings;
in >> paintings;
```