## OpenStack Guides for hosted.meappy.com

#### [OpenStack command-line interface cheat sheet](http://docs.openstack.org/user-guide/cli_cheat_sheet.html)

#### [OpenStack hosted.meappy.com Dashboard](https://secuore.meappy.com/os/)

1. SSH to Jump Host<br>
`[user@local-host ~] ssh -i user_key.pem -p 2233 user@jump-host.hosted.meappy.com`<br>

2. Source Keystone Identity file<br>
`[user@jump-host ~]$ source  keystonerc_user`<br>
`[user@jump-host ~(keystone_user)]$`<br>

3. Issue Nova commands<br>
`[user@jump-host ~(keystone_user)]$ nova list`<br>
`+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`<br>
`| ID                                   | Name         | Status  | Task State | Power State | Networks                    |`<br>
`+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`<br>
`| 37d8cdf4-4079-4b23-acc6-8518c9b771eb | centos2      | SHUTOFF | -          | Shutdown    | int=192.168.1.4             |`<br>
`| 9cdec55e-a3c8-4c38-bdcb-7594eb3db3be | centos6      | ACTIVE  | -          | Running     | int=192.168.1.10, 10.1.1.67 |`<br>
`| 20736923-b1b4-4a49-898c-63fdc007d4d6 | centos6-2    | ACTIVE  | -          | Running     | int=192.168.1.11, 10.1.1.65 |`<br>
`| 2f5e5fca-4128-4a74-b6ec-d103b2b9e932 | instance5    | ACTIVE  | -          | Running     | int=192.168.1.9             |`<br>
`+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`<br>


