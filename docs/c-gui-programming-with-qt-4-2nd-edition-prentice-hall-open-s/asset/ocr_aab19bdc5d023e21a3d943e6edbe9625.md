```
void stop();

signals:
  void bouncing();
```

The AxBouncer constructor is a standard constructor for a widget, with a parent parameter. QAXFACTORY_DEFAULT() macro, which we will use to export the component, expects a constructor with this signature.

The createAggregate() function is reimplemented from QAxBindable. We will explain it in a moment.

protected:

```
  void paintEvent(QPaint event);
  void timerEvent(QTimer event);
```

private:

```
  int intervalInMilliseconds() const;

  QColor ballColor;
  SpeedValue ballSpeed;
  int ballRadius;
  int myTimerId;
  int x;
  int delta;
```

```
};
```

The protected and private sections of the class are the same as those we would have if this was a standard Qt widget.

```
AxBouncer::AxBouncer(QWidget *parent)
  : QWidget(parent)
{
  ballColor = Qt::blue;
  ballSpeed = Normal;
  ballRadius = 15;
  myTimerId = 0;
  x = 20;
  delta = 2;
}
```

The AxBouncer constructor initializes the class's private variables.