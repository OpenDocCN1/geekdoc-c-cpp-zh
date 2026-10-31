the production of an output. Over some range of input rates, the output rate exactly tracks the input rate: The component is performing work at the same rate at which it is being presented with work.

As the input rate increases you eventually reach a point beyond which the component can no longer keep up with the increasing demand. This is the point that defines the operating capacity of the component.

Beyond the operating capacity, you are in the overload region and the behavior of the component is different. Inputs are arriving faster than they are being processed, and either they are being lost altogether or they are piling up in a buffer. If they are piling up in a buffer, that buffer has a finite capacity, and when you reach that capacity something bad is going to happen. Therefore, extended operation in this region is inherently unstable.

But there are consequences for operating in the overload region even before it becomes unstable. Resources that would otherwise be applied to doing useful work with the component are now being dedicated to managing the buffer. Initially, this may just manifest itself as a falling-off of output rate, but as the input rate increases further, the output rate levels off and then begins to decline. It typically declines to some level substantially below the nominal operating capacity of the component.

The bathtub test (or fire hose test) immediately pushes the component well into the overload region. Even though it may be useful in determining whether a component is well behaved (at least for some period of time) when overloaded, it does not give you any true indication of the component’s operating capacity.

# Disabling Features

Another common source of misleading results is running the benchmark test on a component that is not configured as it would be in production. Some common examples are

+   - Using asynchronous disk writes for benchmarking when synchronous interaction will be used in production
+   - Running without security policies in place when security policies will be used in production
+   - Running without transaction management when transactions will be used in production
+   - Running without logging when logging will be used in production