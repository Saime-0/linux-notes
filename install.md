Connect to wifi 

- exec cmd `iwctl` to enter in interactive mode
- exec cmd `station <wlan-name> scan` for start scanning
- exec cmd `station <wlan> connect <network>` for connect to network
- enter password
- ctrl+d

Partiotioning disk

- exec cmd `parted /dev/sdX` to enter in interactiove mode
- exec cmd `mklabel gpt` for create gpt
- exec cmd `mkpart ESP fat32 1MiB 900MiB` for create boot part
- exec cmd `set 1 boot on` fot set boot flag to part
- exec cmd `mkpart primary ext4 900MiB 100%` for create part will using lvm
- exec cmd `quit`

Setup LVM

- exec cmd `pvcreate /dev/sda2` 
