# Conversations

To create a conversation between sprites use “broadcast message and wait” blocks with “say” blocks, which make your sprites talk using speech bubbles. Start a new project and add two monkey sprites to it. Give the script on the left to one monkey, and the two scripts on the right to the other.

```
broadcast message1▼ and wait
```

> △ Waiting blocks
This block sends a message, then waits for all the scripts that react to the message to finish the program continues.

![](bbox=[0.275, 0.281, 0.433, 0.355])

The first monkey starts the conversation

![](bbox=[0.778, 0.323, 0.936, 0.403])

“Say” blocks let your sprites talk using speech bubbles

The “hello” message triggers the second monkey’s script

```
when clicked Hello! for 2 secs
```

The second monkey responds to the first one

```
broadcast hello▼ for 2 secs
```

```
when I receive hello▼
```

```
say How are you? for 2 secs
```

```
say Hi! for 2 secs
```

```
broadcast howareyou▼
```

```
when I receive howareyou▼
```

```
say Great thanks! for 2 secs
```

When the second script ends, the first script continues

![](bbox=[0.083, 0.693, 0.243, 0.763])

The “howareyou” starts the third script

![](bbox=[0.778, 0.733, 0.936, 0.833])

△ Chatty monkeys
This program works because it uses the “broadcast message and wait” block. If the “broadcast message” block was used, the monkeys would talk over each other.