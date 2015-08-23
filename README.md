# openstack-guides

1. SSH to Jump Host
<br />
# ssh -i user_key.pem -p 2233 user@jump-host.hosted.meappy.com

2. Source Keystone Identity file
<br />
[user@jump-host ~]$ source  keystonerc_user
[user@jump-host ~(keystone_user)]$ 

3. Issue Nova commands
`[user@jump-host ~(keystone_user)]$`<br>
`[user@jump-host ~(keystone_user)]$ nova list`<br>
+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+
| ID                                   | Name         | Status  | Task State | Power State | Networks                    |
+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+
| 37d8cdf4-4079-4b23-acc6-8518c9b771eb | centos2      | SHUTOFF | -          | Shutdown    | int=192.168.1.4             |
| 9cdec55e-a3c8-4c38-bdcb-7594eb3db3be | centos6      | ACTIVE  | -          | Running     | int=192.168.1.10, 10.1.1.67 |
| 20736923-b1b4-4a49-898c-63fdc007d4d6 | centos6-2    | ACTIVE  | -          | Running     | int=192.168.1.11, 10.1.1.65 |
| 2f5e5fca-4128-4a74-b6ec-d103b2b9e932 | instance5    | ACTIVE  | -          | Running     | int=192.168.1.9             |
+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`
