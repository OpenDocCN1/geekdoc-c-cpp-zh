queue through specialised enqueue and dequeue functions ensures the indices are maintained, and the accesses are always valid.

```
/* Implements a simple queue of 32-bit ints. */
static int32_t queue_data[QUEUE_SIZE];
static int queue_write_index = 0;
static int queue_read_index = 0;
/* Write data to the queue. Return true if there
 * is space in the queue and the write is
 * successful. */
bool write_queue(int32_t data)
{
    bool success = false;
    /* Check for space in the queue. Then write
     * the data, increment the index, wrapping if
     * necessary. */
    if ((((QUEUE_SIZE + queue_read_index - 1) %
    QUEUE_SIZE) != queue_write_index)
    {
        queue_data[queue_write_index] = data;
        queue_write_index =
        (queue_write_index + 1) % QUEUE_SIZE;
        success = true;
    }
    return success;
}
/* Read data from the queue. Return true if the
 * queue contains some data to read. */
bool read_queue(int32_t * p_data)
{
    bool success = false;
```