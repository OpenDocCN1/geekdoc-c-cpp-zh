Although the queue may be implemented as a simple array, if we wish to add and remove tasks from the queue in a logical manner, using a linked list to store the task handles seems a more logical approach. Each entry in the list therefore stores the task handle and a pointer to the next entry. Interface functions for adding and removing tasks will need to be provided in the scheduler library, but these are no more complicated than the add and remove functions for any other linked list.

```
/* A minimal struct to contain the task list
* entries. */
typedef struct task_s
{
/* Pointer to the next task list entry. */
struct task__s * p_next_task;
/* Pointer to the task reentry point.
* Initialise to the task's entry function.
* Save/restore the CPU's link register
* here. */
void ( * p_reentry)(void);
/* Pointer to the task stack. Initialise to
* the start of the task's stack. Save/restore
* the CPU's stack pointer here. */
char * p_stack;
/* Stored contents of other CPU registers;
* assumes 'int' is same width as a CPU
* register. NUM_GPR is the total number of
* general purpose registers (excludes the
* program counter, stack pointer and link
* registers). */
unsigned int cpu_register[NUM_GPR];
} task_t;
```