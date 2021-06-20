# Memcached

## Installation

1. Download [memcached](https://memcached.org/)
    ```
    >> wget http://www.memcached.org/files/memcached-1.6.9.tar.gz
    >> tar -xzf memcached-1.6.9.tar.gz
    ```


## Memcached and persistent memory

A version of Memcached that uses persistent memory has been developed by Lenovo: https://github.com/lenovo/memcached-pmem

This version was used by Sihang Liu in his paper, [PMFuzz: Test Case Generation for Persistent Memory Programs](https://dl.acm.org/doi/pdf/10.1145/3445814.3446691)
