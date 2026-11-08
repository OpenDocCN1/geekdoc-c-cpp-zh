```
~~~c
        fprintf(stdout, "\nworker thread: working..."); fflush(stdout);
}
void* worker_thread_function(void *arg)
{
    while (1) {
        pthread_mutex_lock(&continue_flag_mutex);
        while (!continue_flag) {
            pthread_cond_wait(&continue_flag_cv, &continue_flag_mutex);
        }
        do_work();
        pthread_mutex_unlock(&continue_flag_mutex);
    }
}
int
main()
{
    pthread_t               worker_thread;
    int                     res = 0;

    continue_flag = 0;
    pthread_mutex_init(&continue_flag_mutex, NULL);
    pthread_cond_init(&continue_flag_cv, NULL);

    res = pthread_create(&worker_thread, NULL, worker_thread_function, NULL);
    if (res != 0) {
        fprintf(stderr, "\nthread creation failed\n");
        return 1;
    }
    while (1) {
        pthread_mutex_lock(&continue_flag_mutex);
        continue_flag = 1;
        pthread_cond_signal(&continue_flag_cv);
        pthread_mutex_unlock(&continue_flag_mutex);
        fprintf(stdout, "\nmain thread: Start work\n"); fflush(stdout);
        sleep(2);
        pthread_mutex_lock(&continue_flag_mutex);
        continue_flag = 0;
        pthread_mutex_unlock(&continue_flag_mutex);
        fprintf(stdout, "\nmain thread: Stop work\n"); fflush(stdout);
        sleep(3);
    }
    fprintf(stdout, "\nwaiting for thread to finish...\n");
    res = pthread_join(worker_thread, NULL);
    if (res != 0) {
        fprintf(stderr, "\nthread join failed\n");
        return 0;
    }
    fprintf(stdout, "\nthread joined. \n");
    pthread_mutex_destroy(&continue_flag_mutex);
    return 0;
}
~~~
```

In the preceding program, instead of using a mutex, we have used the conditional variables to avoid the wastage of CPU cycles.