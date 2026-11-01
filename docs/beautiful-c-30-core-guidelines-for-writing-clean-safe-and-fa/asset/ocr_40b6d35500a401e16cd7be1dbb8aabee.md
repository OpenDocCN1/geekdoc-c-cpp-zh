attempt at producing self-documenting code. For example, if the piece of data was an elevation above sea level, they might name the functions like this:

Click here to view code image

```
/* elevation.h */
void change_height(int new_height);
int height();

/* elevation.c */
int height_ = 0;

void change_height(int new_height)
{
    height_ = new_height;
}

int height()
{
    return height_;
}
```

This would not prevent people from arbitrarily changing heights at inopportune moments throughout the codebase, but at least it would signal what they were doing and perhaps improve client readability by using nouns for functions that queried val-ues and verbs for functions that modified values. Gatekeeping the data in this way allows you to search for its uses, and you get the added bonus of being able to set breakpoints in your debugger so that you can keep a careful watch over it.

However, these were dark times.

# Mere Encapsulation