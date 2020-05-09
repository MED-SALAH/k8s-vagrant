After preaparing machines :
desactivate Swap:
swapof -a
vim /etc/fstab 
comment ligne of swap with #/dev/mapper/.....swap
mount -a

to check : df -hv 