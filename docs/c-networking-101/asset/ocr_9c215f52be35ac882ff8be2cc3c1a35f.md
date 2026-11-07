```
```cpp
int flag;

flag = config["TCP_NODELAY"];

setsockopt(sockfd, IPPROTO_TCP, TCP_NODELAY, &flag,
           sizeof(int));

flag = config["SO_BROADCAST"];

setsockopt(sockfd, SOL_SOCKET, SO_BROADCAST, &flag,
           sizeof(int));

}
```
```

# Recover from Failure

In the event of a failure, we can revert back to our backup configurations:

```
```cpp
void recover_from_failure(int sockfd, const std::string&
backup_filename) {

    nlohmann::json config = read_config(backup_filename);

    apply_config(sockfd, config);

}
```
```