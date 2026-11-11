The return command quits the function, sending back the value specified - in this case 'T'.

# # Lists

Variables can only hold a single value, but sometimes it is useful to be able to collect together a list of things. You will use this example later in the Morse code example. The items in a Lua list can be any type of value. They can be a number or string or even another list.

The example below shows how you can define a list of colors and then print them out one at a time.

```
```lua
colors = {'red', 'orange', 'yellow',
          'green', 'blue',
          'white', 'black'}

for i, color in ipairs(colors) do
  print(color)
end
```
```

In this case, the list is given the values of color names, each as a string. The for loop uses a special command "ipairs" that allows the "for" loop to count with both the position of each thing in the list (i) and the color string (color).

We can prove this by modifying the example so that we print both the position in the list and the string as shown below:

```
```lua
colors = {'red', 'orange', 'yellow',
          'green', 'blue', 'white', 'black'}
for i, color in ipairs(colors) do
  print(i, color)
end
```
```

This will produce an output like this:

```
```
1    red
2    orange
3    yellow
4    green
5    blue
6    white
```
```