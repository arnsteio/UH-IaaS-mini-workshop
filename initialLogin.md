# Log in on the machine we just made

~~~
ssh ubuntu@158.39.75.38
~~~

Update the packages on the machine:

~~~
sudo apt-get -y update
~~~

with `lsblk` we see we don't have a lot of space - and it is, regardless, better to have storage separately so we can attach it to and detach it from machines later. 
Machines are use-and-throwaway, storage is more permanent. 
However, please make sure you have important things backed up!

Let's make some storage, and attach it. 
But we'll do that from the command line, not the web gui.
