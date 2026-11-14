```
void b(...) {
...
void c(...) {
...
void d(...) {
...
void a(...) {
while (...) {
if (...) {
b(...) {
...
}
else (...) {
...
}
d(...) {
...
}
}
}
int main() {
a(...);
d(...);
}
```

![](bbox=[0.38, 0.15, 0.72, 0.39])

FIG. 3.19 Code example and its call graph: (A) C code; (B) Static Call Graph generated from the code in (A). Each node corresponds to a task, with edges denoting the control and data flow between tasks.

Once a call graph has been derived, the next step is to map it to the target heterogeneous architecture. We describe this mapping process for an illustrative heterogeneous embedded platform depicted in Fig. 3.20. This platform contains a CPU as the host processor and a set of hardware accelerators as coprocessors. Each processor has its own local memory with no global shared memory, hence communication is only allowed between the CPU and any of the accelerators. With this type of platform, the CPU runs the application with specific parts of the code (hotspots) offloaded to hardware accelerators to minimize overall execution time.

![](bbox=[0.35, 0.74, 0.58, 0.85])

FIG. 3.20 Block diagram of a possible heterogeneous embedded platform.