```
while ( !happy(science_foundation) ) {
    discretize_model();
    auto my_solver = itl::make_cg_solver(A, PC);
    itl::async_executor async_exec{my_solver};
    async_exec.start_solve(b, x, iter);

    play_with_model();
    if ( found_better_model )
        async_exec.interrupt();
    else
        async_exec.wait();
}
```