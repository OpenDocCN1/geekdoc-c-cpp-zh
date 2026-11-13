# isempty()

Algorithm of isempty() function – 
begin procedure isempty

if front is less than MIN OR front is greater than rear return true
else
return false
endif

end procedure

If the value of **front** is less than MIN or 0, it tells that the queue is not yet initialized, hence empty.

Here's the C programming code –

```
bool isempty() {
if(front < 0 || front > rear) return true;
else
return false;
}
```