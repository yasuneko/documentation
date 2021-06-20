# Redis

Followed instructions from the git repo: https://github.com/redis/redis

1. Clone repo
    ```
    > git clone https://github.com/redis/redis
    ```
1. Make
    ```
    > make
    ```
1. Test
    ```
    > make test
    ```
1. run redis server
    ```
    > cd src
    > ./redis-server
    ```

1. run redis cli
    ```
    > cd src
    > ./redis-cli
    ```

## Redis and persistent memory

Intel pmem has created a version of Redis that uses persistent memory. It can be found at this repository: https://github.com/pmem/redis/tree/3.2-nvml

This version was used by Sihang Liu in his paper, [PMFuzz: Test Case Generation for Persistent Memory Programs](https://dl.acm.org/doi/pdf/10.1145/3445814.3446691)
