```
void move(Point to) override;

void draw() const override;
void rotate(int) override;
```

```
void add_eye(Shape* s)
{
    eyes.push_back(s);
}
```

```
void set_mouth(Shape* s);
virtual void wink(int i); // wink eye number i
```

```
// ...
```

private:
    vector<Shape*> eyes; // usually two eyes
    Shape* mouth;

```
};
```