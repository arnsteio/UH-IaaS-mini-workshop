# UH-IaaS GUI use

*General documentation* on openstack can be found at <http://iaas.readthedocs.io/en/latest/>.

*User documentation* is at <http://docs.uh-iaas.no/en/latest/>.

There is a *public chat room* where you can get help at <https://uhps.slack.com>.

*Issues should be reported* via the GitHub project norcams/iaas: <https://github.com/norcams/iaas/issues>.

## Setup

Before you can use UH-IaaS, you need to do some setup. Please do this only once, if you have done it previously you should drop this step:

1. Go to <https://access.uh-iaas.no/> and follow the steps described at <http://docs.uh-iaas.no/en/latest/login.html#first-time-login>.
   Important - Copy and save the API password! 
   The password for API access is generated and shown here. 
   This is the only time that the API password is generated and shown to you.
2. [Check on your local machine for your SSH keys](https://help.github.com/articles/checking-for-existing-ssh-keys/). 
3. [SKIP THIS STEP IF YOU HAVE AN SSH KEY] If you do not have an SSH key, create a [new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/). 
4. Import your SSH key to openstack. Follow instructions at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#setting-up-a-keypair>.
5. Allow SSH and ICMP access. Follow instructions at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#allowing-ssh-and-icmp-access>.
5. Get familiar with [IaaS dashboard](http://docs.uh-iaas.no/en/latest/dashboard.html).

Subsequent logins should go via <http://dashboard.uh-iaas.no/>.

## Building a machine using the GUI

Go to <https://dashboard.uh-iaas.no/dashboard/project/instances/>, press `Launch instance` and build your machine.
Remember to tick "SSH and ICMP" in the Access & Security tab and choose the correct SSH keypair if you have more than one. 
The IP address of your instance can be found in your "instances" section. 
We can now check if the machine is working. 

## Doing this in CLI instead

Documentation at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#doing-the-same-with-cli>.
In short:

	openstack server list
	openstack keypair list
	openstack security group list

(we have nothing)

Upload an ssh key:

	 openstack keypair create --public-key ~/.ssh/id_rsa.pub Dell_XPS15

Create security group:

	openstack security group create --description "Allow incoming SSH and ICMP" SSH_and_ICMP
	openstack security group rule create --src-ip 0.0.0.0/0 --dst-port 22 --protocol tcp --ingress SSH_and_ICMP
	openstack security group rule create --src-ip 0.0.0.0/0 --protocol icmp --ingress SSH_and_ICMP

Getting the info we need; images, favours, networks

	openstack image list
	openstack flavor list
	openstack network list

Making a server:

	openstack server create --image "Fedora 25" --flavor m1.small --security-group SSH_and_ICMP --security-group default --key-name Dell_XPS15 --nic net-id=osl-public myserver
