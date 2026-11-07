```
```c
int r = uv_listen((uv_stream_t*) &server, DEFAULT_BACKLOG, on_new_connection);

if (r) {

    fprintf(stderr, "Listen error: %s\n", uv_strerror(r));

    return 1;

}

return uv_run(uv_default_loop(), UV_RUN_DEFAULT);

}
```
```

This code starts a server on port 7000 and echos back whatever data is sent to it.