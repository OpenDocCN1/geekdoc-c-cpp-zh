```
if (Views[i]->clearTargets)
{
    ClearTarget (Views[i]->clearFlags,
    Views[i]->clearColor, Views[i]->clea
}

for (int k = 0; k < Views[i]->commands.siz
executeDrawCommand (Views[i]->commands[k
}
}
}
```

In addition, Listing 10.7 highlights a very important aspect of serialization of RenderView objects, namely that some RenderView objects are dependent on others, so even though we're compositing them in multiple threads, we must still submit them in a particular order to the API. For instance, you need to composite shadow maps before you can use them in subsequent draw commands.