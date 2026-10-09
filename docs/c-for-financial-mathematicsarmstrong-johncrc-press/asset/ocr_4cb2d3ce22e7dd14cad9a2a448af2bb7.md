both threads repeat their calculations in a loop, this will result in two threads simultaneously performing the overall calculation.

As an example of a the code used to write, here is an example of a Write-Task:

```
class WriteTask : public Task {
public:
Pipeline& pipeline;
void execute() {
for (int i=0; i<100; i++) {
pipeline.write(i);
}
}
WriteTask( Pipeline& pipeline ) :
pipeline( pipeline ) {
}
};
```

In a similar way one can write a ReadTask:

```
class ReadTask : public Task {
public:
Pipeline& pipeline;
double total;
void execute() {
for (int i=0; i<100; i++) {
total+=pipeline.read();
}
}
ReadTask( Pipeline& pipeline ) :
pipeline( pipeline ),
total(0.0 ) {
}
};
```

Using an Executor we can run these two tasks simultaneously.

```
static void testTwoThreads() {
Pipeline pipeline;
auto w = make_shared<WriteTask>( pipeline );
auto r = make_shared<ReadTask>( pipeline );
SPExecutor executor = Executor::newInstance(2);
executor->addTask( r );
```