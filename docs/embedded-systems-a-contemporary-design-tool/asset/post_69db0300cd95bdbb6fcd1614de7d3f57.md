
For a single periodic task, CPU utilization is given as

| | |
|---|---|
| \( u_i = e_i / P_i \) | |
| \( u_i \) | fraction of time task keeps CPU busy |
| \( e_i \) | execution time |
| \( P_i \) | for periodic task is the period |

One can express a similar relationship for aperiodic tasks.

CPU utilization information can be used in conjunction with a sequence diagram to aid in assessing when each of the tasks can and needs to run.

## 12.3.2 Scheduling Decisions

Two key elements of real-time design – repeatability and predictability – are absolutely essential in the context of hard deadlines. To ensure predictability, one must completely understand and define the timing characteristics of each task and properly schedule those tasks using a predictable scheduling algorithm. The first step in developing a robust schedule is knowing when a scheduling decision must be made.

Scheduling decisions are made under the following four conditions:

- 1. A process switches from the *running* to the *waiting* state – initiated by an I/O request.
- 2. A process switches from the *running* to the *ready* state – when an interrupt occurs.
- 3. A process switches from the *waiting* to the *ready* state – the completion of I/O activity.
- 4. A process terminates.

If only conditions 1 and 4 are used to make a scheduling decision, such scheduling is called *nonpreemptive*. Under such scheduling criteria, a process keeps the CPU until it decides to release, that is, when it terminates or switches to the waiting state. Otherwise, the schedule is called *preemptive*.

## 12.3.3 Scheduling Criteria

Today there are a great number of different scheduling algorithms. When making a choice, one must consider the properties of the various algorithms coupled with what is considered important or essential for the specific application. In the following sections, we identify several of the more common metrics. The list is, by no means, complete, nor is it universally applicable.

### 12.3.3.1 Priority

In a design that utilizes priority as a part of the scheduling criteria, the designer must critically assess each task in the system to establish the appropriate priority. The scheduler utilizes such information at several different times. If no task is running or if a task terminates, the highest priority task among the tasks that are ready will be selected to run next. Under a preemptive scheduling policy, if a lower priority task is executing when a higher priority task arrives, the arriving task preempts the executing task. The lower priority task is then suspended. The suspended task resumes when the higher priority task completes or blocks waiting for some resource. If no task with a higher priority ever arrives, the executing task runs to completion.

**blocking** Although a priority scheme seems to ensure that the most important tasks will always complete, such is not always the case. With preemption, the problem of blocking arises. Blocking occurs when a task needs a resource that is owned by another task. Consider several examples.

- **Case 1**
- 1. Task A has higher priority than Task B.
- 2. Task B starts and reserves Resource R1.
- 3. Task A preempts Task B.
- 4. Task A begins execution and becomes blocked at the point that Resource R1 is needed.
- 5. Task A must suspend and allow B to complete, thereby releasing R1.

**priority inversion** A second case introduces a problem called *priority inversion*. A problem of this nature occurred on one of the Mars missions. (Please see Chapter 8 on safety and reliability.)

- **Case 2**
- We have three tasks: Task A, Task B, and Task C.
- Task A has the highest priority and Task C the lowest.
- 1. Task C starts and reserves Resource R1.
- 2. Task A enters and preempts Task C.
- 3. Task A begins execution and becomes blocked at the point that Resource R1 is needed.
- 4. Task A must suspend and allow C to continue, hopefully releasing R1.
- 5. Task B preempts Task C and does not need R1.
- 6. Task B completes and allows Task C to resume.

It is easy to create a situation in which the highest priority task is blocked forever. A high priority task that can be scheduled in isolation may fail in a multitasking context. In a hard real-time context, one must ensure a bound on priority inversion.

### 12.3.3.2 Turnaround Time

*Turnaround time* specifies the interval from the time of the submission of a task until its completion. Included is the time spent waiting to get into memory, the time waiting in the ready queue, and the time spent executing on the CPU or doing I/O.

### 12.3.3.3 Throughput

**Throughput** Coupled with turnaround time is *throughput*, the number of processes that are completed per unit of time. Throughput depends, of course, on the complexity of the task. One should be careful when working with a throughput metric. A system may exhibit a very high throughput, but if the turnaround time is excessive we may not be able to meet our timeliness constraints.

### 12.3.3.4 Waiting Time

In embedded applications built around a kernel or full OS, the path a task takes through the system involves a number of different queues. When a user or system task initially enters the system, it is put into an entry queue. When all of its necessary conditions are satisfied such that it can run when the CPU is available, it is placed in a ready queue. Tasks may also arrive at the ready queue via other paths as well – for example, if they have been interrupted by a higher priority task or if they have blocked on an I/O operation that has completed. When a process is put into the ready queue, it waits until it is selected for execution. At such a time, it is dispatched – given the CPU to execute.

During execution, the process may issue an I/O request and be placed in an I/O queue, request a resource that may not be immediately available, or create new subprocess(es) and wait for their termination. Processes waiting for a particular resource may be placed in the queue for that resource. That queue is often called a device queue. When a process is terminated, it is removed from all queues. Its TCB and all resources are deallocated.

### 12.3.3.5 Response Time

Response time is yet another consideration. For an interactive system, turnaround time may not be the best measure. Instead, the time from submission to first response is considered. The time taken for the first response is not the time to the first output.

## 12.4 SCHEDULING ALGORITHMS

- asynchronous interrupt event driven, polled, and polled with a timing event

Although it is beyond the scope of this text to go into details of all the many scheduling algorithms, it is informative to look at a number of them. Several of the very simplest include asynchronous interrupt event driven, polled, and polled with a timing event. With such algorithms, the control strategy is architected to support one or a few tasks. Scheduling and dispatch are automatic. Intertask communication either does not exist or it relies on global variables. Though simple, such algorithms can be essential in cases with hard deadlines.

### 12.4.1 Asynchronous Interrupt Event Driven

One of the simplest scheduling schemes is asynchronous interrupt event driven. Certainly, the asynchronous nature of the scheme calls into question the use of the word “schedule.” Under such an approach, the system is constrained to operate in a basic one-line infinite loop until an interrupting event occurs, as is illustrated in the code fragment shown in Figure 12.4.

```
global variable declarations

isr set up
function prototypes
void main (void)
{
    local variable declarations
    while(1);     //task loop
}
ISRs
function definitions
```

Figure 12.4 An Event-driven Schedule Algorithm.

As such, the design is a special case of the foreground/background model. In this case, the design has no background tasks. The design can also be considered to be reactive.

When an interrupting event occurs, flow of control jumps to the associated Interrupt Service Routine (ISR), where the designated task is executed; flow then resumes in the infinite loop. Generally, the event originates from some external source. We will look at an extension to the event-driven approach in which the event derives from a system timer.

The overall behavior of such a system can be difficult to analyze because of the non-deterministic nature of asynchronous interrupts. However, it is rather straightforward to determine the post-event behavior for systems with a single interrupt or the behavior of the highest priority interrupt in systems with more than one interrupt.

### 12.4.2 Polled and Polled with a Timing Element

The basic polled algorithm is among the simplest and fastest algorithms. The system continually loops, waiting for an event to occur. The difference between the polled algorithm and the event driven is that the polled algorithm is continually testing the value of the polled signal looking for a state change. The interrupt-driven design, on the other hand, does nothing until the event occurs. Only then does it respond. Schematically, the algorithm is given as shown in Figure 12.5.

```
global variable declarations
function prototypes
void main (void)
{
    local variable declarations
    while(1) // task loop
    {
        // test state of each signal in polled set
        if then construct
        or
        switch statement
    }
}
function definitions
```

Figure 12.5 A Polling-based Schedule Algorithm.

Such a scheme works well for a single task. It is completely deterministic. The time to respond to the event is computable and bounded. In the worst case, let's assume the event occurs immediately after the test instruction. Under such a circumstance, the response time is the length of the loop. Polled with a timing element is a simple extension. The scheme uses a timing element to ensure a delay action after a polled event is true. Such a technique deskews the incoming signals.

The polled model is also a special case of the foreground/background model. In contrast to the event-driven schedule, the polled model has no foreground tasks. The design implements a reactive system.

### 12.4.3 State Based

The next approach implements the flow of control through the task set as a finite automaton or state machine. The two basic implementations of the finite-state machine (FSM), Mealy and Moore, are distinguished by the implementation of the output function: in Mealy the
