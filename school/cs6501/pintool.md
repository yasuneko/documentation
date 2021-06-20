## Install virtualbox-6.1

1. Determine os:

    https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/

    ```
    > cat /etc/os-release
    ```

1. https://www.virtualbox.org/wiki/Linux_Downloads Add repo to source list
    ```
    > sudo vim /etc/apt/sources.list
    > deb https://download.virtualbox.org/virtualbox/debian <mydist> contrib
    > sudo apt-get update
    > sudo apt-get install virtualbox-6.1
    ```

1. Download mint linux:
    https://drive.google.com/file/d/1jdQidqCsb-_yQOiMq6VjUk97kYSwNUHq/view

1. Transfer using scp
    ```
    > scp ~/Downloads/Linux\ Mint.ova 192.168.4.66:/home/yasuneko/repos/cs6501_cyber_forensics
    ```

1. Import image: https://www.techrepublic.com/article/how-to-import-and-export-virtualbox-appliances-from-the-command-line/
    ```
    > vboxmanage import Linux Mint.ova
    ```

1. Show vm list:
    ```
    > vboxmanage list vms
    ```

1. Start vm:
    ```
    > vboxmanage startvm "Linux Mint" --type=headless
    ```

1. Connect to vm:
    ```
    > ssh -p 2200 swsec19@127.0.0.1
    ```

1. Stop vm:
    ```
    > vboxmanage controlvm "Linux Mint" poweroff soft
    ```

1. Set vm to bridged mode:
    ```
    > ifconfig
    >  vboxmanage modifyvm "Linux Mint" --nic1 bridged --bridgeadapter1 enp2s0f0
    > vboxmanage modifyvm "Linux Mint" --nic1 bridged --nictype1 82545EM --bridgeadapter1 enp2s0f0
    ```

1. Find ip address:
    ```
    > sudo arp-scan -l
    ```

1. Connect from outside:
    ```
    > ssh swsec19@192.168.4.69
    ```
