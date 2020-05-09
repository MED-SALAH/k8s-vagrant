vagrant init
vagrant status
vagrant up -- to start the install of machines

To access to machine : vagrant ssh "nameofmachine"
example:
vagrant ssh kubmaster 

Or you can use vagrant private key for eache machine:
vagrant ssh-config

After preaparing machines :

desactivate Swap:
swapof -a
vim /etc/fstab 
comment ligne of swap with #/dev/mapper/.....swap
mount -a

to check : df -hv 

Nos machines have alerady docker installed in Vagrantfile
add docker user to group sudo :
sudo usermod -aG docker SUSER

