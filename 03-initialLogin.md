# Log in on the machine we just made

The IP address of your instance can be found in your "instances" section.
You log in as user "ubuntu" for ubuntu, "fedora" for fedora:
~~~
ssh ubuntu@158.39.75.38
~~~

You might need to include ssh keys explicitly:  `ssh -i $HOME/.ssh/id_rsa ubuntu@158.39.75.38`

Update the packages on the machine after you have logged in:

~~~
sudo apt-get -y update
~~~

with `lsblk` we see we don't have a lot of space - and it is, regardless, better to have storage separately so we can attach it to and detach it from machines later. 
Machines are use-and-throwaway, storage is more permanent (although backup is still important!).

Let's make some storage, and attach it. 
But we'll do that from the command line, not the web gui.
