# UH-IaaS GUI use

General documentation on openstack can be found [here](http://iaas.readthedocs.io/en/latest/).
User documentation is at <http://docs.uh-iaas.no/en/latest/>.

## Setup

Before you can use UH-IaaS, you need to do some setup. Please do this only once, if you have done it previously you should drop this step:

1. Go to <https://access.uh-iaas.no/> and follow the steps described at <http://docs.uh-iaas.no/en/latest/login.html#first-time-login>.
2. [Check on your local machine for your SSH keys](https://help.github.com/articles/checking-for-existing-ssh-keys/). 
3. [SKIP THIS STEP IF YOU HAVE AN SSH KEY] If you do not have an SSH key, create a [new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/). 
4. Import your SSH key to openstack. Follow instructions at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#setting-up-a-keypair>.
5. Allow SSH and ICMP access. Follow instructions at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#allowing-ssh-and-icmp-access>.
5. Get familiar with [IaaS dashboard](http://docs.uh-iaas.no/en/latest/dashboard.html).

## Building a machine using the GUI

Go to <https://dashboard.uh-iaas.no/dashboard/project/instances/>, press `Launch instance` and build your machine.
Remember to tick "SSH and ICMP" in the Access & Security tab and choose the correct SSH keypair if you have more than one. 
The IP address of your instance can be found in your "instances" section. 
We can now check if the machine is working. 
