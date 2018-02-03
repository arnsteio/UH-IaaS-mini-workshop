# Attaching storage

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

`openstack volume list` could be helpful wrt mounting the storage .

OK, let's now go back to the machine.
