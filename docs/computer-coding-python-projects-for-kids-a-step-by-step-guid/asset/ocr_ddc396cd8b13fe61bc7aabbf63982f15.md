# ### 8 Draw the arms

Each arm is drawn in two parts: first the upper arm, from the robot's shoulder to its elbow; then the lower arm, from the elbow to the wrist. Type this below the code you added in Step 7, then run it to see the arms appear.

```
```python
# arms
t.goto(-150, 70)
rectangle(60, 15, 'grey')
t.goto(-150, 110)
rectangle(15, 40, 'grey')

t.goto(10, 70)
rectangle(60, 15, 'grey')
t.goto(55, 110)
rectangle(15, 40, 'grey')
```
```

Upper right arm

Lower right arm

Upper left arm

Lower left arm

# ### 9 Draw the neck

Time to give your robot a neck. Type these neck-drawing commands below the code you added in Step 8.

```
```python
# neck
t.goto(-50, 120)
rectangle(15, 20, 'grey')
```
```

# ### 10 Draw the head

Oops - you've drawn a headless robot! To give your poor robot a head, type these commands below the code you added in Step 9.

```
```python
# head
t.goto(-85, 170)
rectangle(80, 50, 'red')
```
```

Don't forget to save your work.

![](bbox=[0.09, 0.72, 0.91, 0.98])