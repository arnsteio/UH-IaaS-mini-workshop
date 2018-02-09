# UH-IaaS documentation

*General documentation* on openstack can be found at <http://iaas.readthedocs.io/en/latest/>.

*User documentation* is at <http://docs.uh-iaas.no/en/latest/>.

There is a *public chat room* where you can get help at <https://uhps.slack.com>.

*Issues should be reported* via the GitHub project norcams/iaas: <https://github.com/norcams/iaas/issues>.

## API password

Before you can use UH-IaaS, you need to do some setup.
Go to <https://access.uh-iaas.no/> and follow the steps described at <http://docs.uh-iaas.no/en/latest/login.html#first-time-login>.

	Important - Copy and save the API password! 
   	The password for API access is generated and shown here. 
   	This is the only time that the API password is generated and shown to you.

## Initializing, and building a machine using the GUI

1. [Check on your local machine for your SSH keys](https://help.github.com/articles/checking-for-existing-ssh-keys/). 
2. [SKIP THIS STEP IF YOU HAVE AN SSH KEY] If you do not have an SSH key, create a [new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/). 
3. Import your SSH key to openstack. Follow instructions at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#setting-up-a-keypair>.
4. Allow SSH and ICMP access. Follow instructions at <http://docs.uh-iaas.no/en/latest/create-virtual-machine.html#allowing-ssh-and-icmp-access>.
5. Go to <https://dashboard.uh-iaas.no/dashboard/project/instances/>, press `Launch instance` and build your machine.
   Remember to tick "SSH and ICMP" in the Access & Security tab and choose the correct SSH keypair if you have more than one. 

Subsequent logins should go via <http://dashboard.uh-iaas.no/>.

The IP address of your instance can be found in your "instances" section. 

## For CLI work: Installing openstack-cli
You need to install openstack-client. You can either do it directly in the OS, or via Python.
Something along these lines
~~~
apt-get install openstack-cli

or

apt install python3-openstackclient

or

apt install python-dev python-pip
pip install python-openstackclient

or

C:\>easy_install pip
~~~

Check the installation: 
~~~
arnsteio@☠:~$ which openstack
/usr/bin/openstack
arnsteio@☠:~$ openstack --version
openstack 2.3.1
~~~
2.3.1 is OK, but e.g. Ubuntu has a more recent Snap:
~~~
arnsteio@☠:~$ which openstack-cli 
/snap/bin/openstack-cli
arnsteio@☠:~$ openstack-cli --version
openstack 3.11.0
~~~

## Make keystone.rc setup file:
~~~
arnsteio@☠:~$ cat keystone_rc.sh 
export OS_USERNAME=arnstein.orten@geo.uio.no
export OS_PROJECT_NAME=DEMO-arnstein.orten.geo.uio.no
export OS_PASSWORD=<API-password-from-1st-login>
export OS_AUTH_URL=https://api.uh-iaas.no:5000/v3
export OS_IDENTITY_API_VERSION=3
export OS_USER_DOMAIN_NAME=dataporten
export OS_PROJECT_DOMAIN_NAME=dataporten
#export OS_REGION_NAME=bgo
export OS_REGION_NAME=osl
export OS_NO_CACHE=1
~~~

Testing whether it works at all:
~~~
arnsteio@☠:~$ . keystone_rc.sh 
arnsteio@☠:~$ openstack server list

arnsteio@☠:~$
~~~

No error message - we're good :-)

`openstack limits show --absolute|grep max` can also be useful. 

## Initializing, and building a machine using CLI

Verifying that we have nothing:

	openstack server list
	openstack keypair list
	openstack security group list


Upload an ssh key:

	 openstack keypair create --public-key ~/.ssh/id_rsa.pub Dell_XPS15

Create security group:

	openstack security group create --description "Allow incoming SSH and ICMP" SSH_and_ICMP
	openstack security group rule create --remote-ip 0.0.0.0/0 --dst-port 22 --protocol tcp --ingress SSH_and_ICMP
	openstack security group rule create --remote-ip 0.0.0.0/0 --protocol icmp --ingress SSH_and_ICMP

If you have problems, `openstack security group rule create --help` might help. 
On old `openstack-cli` installs, `openstack security group rule create --src-ip 0.0.0.0/0 --proto icmp  SSH_and_ICM` might work.

Getting the info we need; images, flavours, networks

	openstack image list | grep -v deactivated
	openstack flavor list
	openstack network list

Making a server:

	openstack server create --image "GOLD Fedora 27" --flavor m1.small --security-group SSH_and_ICMP --security-group default --key-name Dell_XPS15 --nic net-id=dab01c68-c25d-4051-ad5b-7b7b07f16f05 myTestServer


We can now check if the machine is working. 
