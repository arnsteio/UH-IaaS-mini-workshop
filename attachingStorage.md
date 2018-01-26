# Attaching storage

We want to make and attache the storage from the command line, not the gui.

## Installing openstack-cli
You need to install openstack-client. YOu can either do it directly in the OS, or via Python.
Something along these lines
~~~
apt-get install openstack-cli

apt install python-dev python-pip
pip install python-openstackclient

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
export OS_PASSWORD=<API-password-from.1st-login>
export OS_AUTH_URL=https://api.uh-iaas.no:5000/v3
export OS_IDENTITY_API_VERSION=3
export OS_USER_DOMAIN_NAME=dataporten
export OS_PROJECT_DOMAIN_NAME=dataporten
#export OS_REGION_NAME=bgo
export OS_REGION_NAME=osl
export OS_NO_CACHE=1
~~~

Testing wether it works at all:

~~~
arnsteio@☠:~$ . keystone_rc.sh 
arnsteio@☠:~$ openstack server list
+--------------------------------------+----------+--------+-----------------------------------------------+
| ID                                   | Name     | Status | Networks                                      |
+--------------------------------------+----------+--------+-----------------------------------------------+
| c0b5b96d-7e5b-41a0-9309-aa78d54bf530 | 3D-build | ACTIVE | dualStack=158.39.75.38, 2001:700:2:8200::2059 |
+--------------------------------------+----------+--------+-----------------------------------------------+
~~~

We're good :-)

## Making storage
~~~
arnsteio@☠:~$ openstack volume create --size 10 --description "Testvolum" mittTestVolum
+---------------------+--------------------------------------+
| Field               | Value                                |
+---------------------+--------------------------------------+
| attachments         | []                                   |
| availability_zone   | nova                                 |
| bootable            | false                                |
| consistencygroup_id | None                                 |
| created_at          | 2018-01-26T12:42:31.045768           |
| description         | Testvolum                            |
| encrypted           | False                                |
| id                  | 365048fe-7cd9-4da5-a96f-470cad39937b |
| multiattach         | False                                |
| name                | mittTestVolum                        |
| properties          |                                      |
| replication_status  | disabled                             |
| size                | 10                                   |
| snapshot_id         | None                                 |
| source_volid        | None                                 |
| status              | creating                             |
| type                | None                                 |
| updated_at          | None                                 |
| user_id             | cee3e5fd16f74f0f8a86ce98e0fd6dc6     |
+---------------------+--------------------------------------+
arnsteio@☠:~$ openstack server add volume 3D-build mittTestVolum
arnsteio@☠:~$ 
~~~

OK, let's now go to the machine itself.
