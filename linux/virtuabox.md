# VirtualBox

## Delete virtualbox
```
> vboxmanage unregistervm "<VBOX_NAME>"
```


## Attach vmdk to virtualbox instance using vboxmanage
Open _.vbox_ file. Look for "StorageController" section, and find the controller with "AttachedDevice".

Run the following command:
```
> vboxmanage storageattach <VBOX_NAME> --storagectl <STORAGE_CONTROLLER_NAME> --device 0 --port 0 --type hdd --medium "<VMDK_LOCATION>" 
```