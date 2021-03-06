**1. Tạo DB và gán quyền**
```
MariaDB [(none)]> CREATE DATABASE placement;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> GRANT ALL PRIVILEGES ON placement.* TO 'placement'@'localhost' \
    ->   IDENTIFIED BY '123456';
Query OK, 0 rows affected (0.000 sec)

MariaDB [(none)]> GRANT ALL PRIVILEGES ON placement.* TO 'placement'@'%' \
    ->   IDENTIFIED BY '123456';
Query OK, 0 rows affected (0.000 sec)
```
**2. Tạo User và Endpoint**
- Tạo User
```
root@controller:~# openstack user create --domain default --password-prompt placement
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | f42a42bfa46a4363bcfb022a9428fd4d |
| name                | placement                        |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+
```
- Add role cho user
```
openstack role add --project service --user placement admin
```
- Tạo Placement API entry trong service catalog
```
root@controller:~#  openstack service create --name placement \
>   --description "Placement API" placement
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | Placement API                    |
| enabled     | True                             |
| id          | da8382f82c614cf090d83c369b7c4c26 |
| name        | placement                        |
| type        | placement                        |
+-------------+----------------------------------+
```
- Tạo Placement API Service endpoint
```
root@controller:~# openstack endpoint create --region RegionOne   placement public http://controller:8778
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 91888ed579dd4297adf59869c9dd1ef7 |
| interface    | public                           |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | da8382f82c614cf090d83c369b7c4c26 |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+
root@controller:~# openstack endpoint create --region RegionOne \
>   placement internal http://controller:8778
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 0275edb0e5324423b577715ca9fa8a1d |
| interface    | internal                         |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | da8382f82c614cf090d83c369b7c4c26 |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+
root@controller:~# openstack endpoint create --region RegionOne \
>   placement admin http://controller:8778
+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | ac03dab6629b4b8dbb29503d28ad88c4 |
| interface    | admin                            |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | da8382f82c614cf090d83c369b7c4c26 |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+

```
- Cài đặt 
```
apt install placement-api
``` 
- Cấu hình file `/etc/placement/placement.conf`
```
[placement_database]
connection = mysql+pymysql://placement:123456@controller/placement

[api]
auth_strategy = keystone

[keystone_authtoken]
auth_url = http://controller:5000/v3
memcached_servers = controller:11211
auth_type = password
project_domain_name = Default
user_domain_name = Default
project_name = service
username = placement
password = 123456
```
- Lưu vào DB
```
/bin/sh -c "placement-manage db sync" placement
```
- Restart apache
```
service apache2 restart
```