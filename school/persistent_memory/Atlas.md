# ATLAS
## HOW TO INSTALL ATLAS
Make sure you are using Ubuntu 16.04

1. Install dependencies
    ```
    > sudo apt-get update
    > sudo apt-get install clang
    > sudo apt-get install llvm
    > sudo apt-get install clang-3.6
    > sudo apt-get install ruby
    > update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.6 100
    > update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.6 100
    > update-alternatives --install /usr/bin/llvm-config llvm-config /usr/bin/llvm-config-3.6 100
    > apt-get install git
    > apt-get install cmake
    > apt-get install libboost-graph-dev
    ```

1. Clone git repo
    ```
    > git clone https://github.com/HewlettPackard/Atlas.git
    ```

1. Build NVM instrumentor
    ```
    > cd compiler-plugin
    > ./build_plugin
    ```

1. Build Atlas
    ```
    > cd runtime
    > mkdir build-all
    > cd build-all
    > cmake ..
    > make
    ```

1. Run Tests
    ```
    > tests/run_quick_test
    ```

## Pointers for exploring the repository:

* Run specific test
    ```
    > ./tests/data_structures/stores_nvm
    ```

* Persistent log location is `/dev/shm/yasuneko/regions/`
* If "Region exists" error, remove region from above directory and delete `__nvm_region_table`

* Crash and recover specific test
    ```
    > cmake .. -DFORCE_FAIL=true
    > make
    > ./tests/data_structures/stores_nvm
    > ./tools/recover stores_nvm
    > cmake .. -DFORCE_FAIL=false
    > make
    > ./tests/data_structures/stores_nvm
    ```