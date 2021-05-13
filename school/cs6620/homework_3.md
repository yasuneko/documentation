1. Install Docker on server
    Follow instructions found [here](https://docs.docker.com/engine/install/ubuntu/)

    1. remove possible old files
        ```
        >>  sudo apt-get remove docker docker-engine docker.io containerd runc
        ```

    1. Install some packages
        ```
        >> sudo apt-get update
        >> sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
        ```

    1. Something something GPG key
        ```
        >> curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
        ```

    1. More commands
        ```
        >> echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        ```

    1. Install docker engine
        ```
        >> sudo apt-get update
        >> sudo apt-get install docker-ce docker-ce-cli containerd.io
        ```

    *** ISSUE ***

    Got error:
    ```
    docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create: dial unix /var/run/docker.sock: connect: permission denied.
    See 'docker run --help'.
    ```

    When attempting to run
    ```
    >> docker run hello-world
    ```

    The fix is described [here](https://docs.docker.com/engine/install/linux-postinstall/)
    
    1. create docker group
        ```
        >> sudo groupadd docker
        ```
    
    1. Add yourself to the group
        ```
        >> sudo usermod -aG docker $USER
        ```
    
    1. log out and log back in

1. Get ubuntu image and run

    Some documentation:
    * https://docker-curriculum.com/
    * https://serverfault.com/questions/661909/the-right-way-to-keep-docker-container-started-when-it-used-for-periodic-tasks

    ```
    >> docker pull ubuntu
    >> docker run -it --name <NAME> ubuntu
    >> docker ps -a                 //Check docker container id
    >> docker start <CONTAINER ID>  //Start Docker Container
    ```

1. Enable remote access of docker
    This is used so I can access the docker container from VS Code

    Documentation found [here](https://www.ivankrizsan.se/2016/05/18/enabling-docker-remote-api-on-ubuntu-16-04/)
    1. edit file
        ```
        >> sudo vim /lib/systemd/system/docker.service
        ```
        Modify the following line
        ```
        >> ExecStart=/usr/bin/docker daemon -H fd:// -H tcp://0.0.0.0:4243
        ```
    1. Restart Docker
        ```
        >> systemctl daemon-reload
        >> sudo service docker restart
        ```

    1. Check that docker api is working
        ```
        >> curl http://localhost:4243/version
        ```

    If ssh keys are set up properly, the VSCode docker app should recognize the new context and connect.

1. Clone homework repo
    ```
    >> apt-get update
    >> apt install cmake
    >> apt install build-essential
    >> apt install pkg-config
    ```
    Instructions are on the repo site: https://github.com/matthewbdwyer/tipc-passes
    ```
    >> git clone git@github.com:matthewbdwyer/tipc-passes.git
    >> apt install libllvm-11-ocaml-dev libllvm11 llvm-11 llvm-11-dev llvm-11-doc llvm-11-examples llvm-11-runtime llvm-11-tools libclang-common-11-dev
    ```
    ```
    >> sudo ln -s /usr/bin/llvm-config-11 /usr/local/bin/llvm-config
    ```

1. Install tipc

    ```
    >> apt install lsb-release
    >> apt install software-properties-common
    ```

    ```
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A122542AB04F24E3
    ```