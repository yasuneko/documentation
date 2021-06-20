https://linuxhint.com/exfat_compatibility_ubuntu/

1.  install exfat-utils
    ```
    > sudo apt install exfat-utils
    ```
1. list all drives
    ```
    > sudo lsblk
    ```

1. Give device GPT label
    ```
    > sudo parted -a optimal /dev/<DEVICE_NAME>
    (parted) mklabel gpt
    (parted) print
    (parted) quit
    ```

1. format drive using mkfs
    ```
    > sudo mkfs.exfat /dev/<DEVICE_NAME>
    ```

1. mount drive
    ```
    > sudo mkdir /media/newhd
    > sudo mount /dev/<DEVICE_NAME> /media/newhd
    ```

1. Auto mount drive
    Information can be found here: https://help.ubuntu.com/community/AutomaticallyMountPartitions


    1. get drive info
        ```
        > sudo fdisk -l
        ```
    
    1. Determine device UUID
        ```
        > sudo blkid
        ```
    
    1. Edit /etc/fstab
        ```
        > sudo vim /etc/fstab

        UUID=<DEVICE UUID> <MOUNT POINT> exfat-fuse defaults 0 0
        ```
    
    1. 


# add line for ntfs drive
