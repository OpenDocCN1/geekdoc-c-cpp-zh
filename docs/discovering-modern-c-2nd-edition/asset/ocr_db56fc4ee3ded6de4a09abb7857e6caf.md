```
void start_solve(const VectorB& b, VectorX& x,
             Iteration& iter) const
{
    my_iter.set_iter(iter);
    my_thread = std::thread(
        [this, &b, &x ]() {
            my_solver. solve(b, x, my_iter);}
    );
}
int wait() {
    my_thread. join();
    return my_iter. error_code();
}
int interrupt() {
    my_iter.interrupt();
    return wait();
}
bool finished() const { return my_iter.iter .finished(); }
}
private:
    Solver
    my_solver;
    mutable interruptible_iteration my_iter ;
    mutable std::thread my_thread ;
};
```

After a solver is started with the `async_executor`, we can work on something else and check from time to time whether the solver is `finished()`. If we realize that the result has become irrelevant, we can `interrupt()` the execution. For both the complete solution and the interrupted execution, we must `wait()` until the `thread` is properly finished with `join`.

The following pseudo-code shows how scientists could use this asynchronous execution:

Click here to view code image

```
while ( 'happy(science_foundation) ) {
    discretize_model();
    auto my_solver = itl::make_cg_solver(A, PC);
    itl::async_executor async_exec (my_solver);
    async_exec.start_solve (b, x, iter);

    play_with_model ();
    if ( found_better_model ) {
        async_exec.interrupt();
    }
    else
```