Looking through, we see cmp statements. The first cmp statement compares
ecx to zero. If ecx is not zero, we go to _Label_1, decrement eax, and then
fall through to _Label_2. If ecx is zero, we increment eax, and go directly to
_Label_2. Writing out some pseudocode, we have the following result for the first section:

```
if(ecx does equal 0) goto _label_1
eax++;
goto _label_2
:_label_1
eax--;
:_label_2
```

Since, _Label_2 occurs at the end of this structure, we can rename it to something more
descriptive, like 'End_of_Branch_1', or 'Branch_1_End'. The first comparison tests
ecx against 0, and jumps on not-equal. We can reverse the conditional, and say
that _Label_1 is an else block:

```
if(ecx == 0); ecx is param1
{
eax++;
}
else
{
eax--;
}
```

So we can rename _Label_1 to something else descriptive, as 'Else_1'. The rest of
the code block, after Branch_1_End (_Label_2) is as follows:

```
mov ecx, [ebp + 12]
cmp ecx, 0
jne _Label_3
inc eax
:_Label_3
```

We can see immediately that _Label_3 is the end of the branch structure, so we can
immediately call it 'Branch_2_End', or something else. Here, we are again comparing
ecx to 0, and if it is not equal, we jump to the end of the block. If it is equal to zero,
however, we increment eax, and fall out the bottom of the branch. We can see that
there is no else block in this branch structure, so we don't need to invert the condition.
We can write an if statement directly:

```
if(ecx == 0); ecx is param2 here
{
```