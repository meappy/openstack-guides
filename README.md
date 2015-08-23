## OpenStack Guides for hosted.meappy.com

##### Links
- [OpenStack command-line interface cheat sheet](http://docs.openstack.org/user-guide/cli_cheat_sheet.html)
- [ Floating IPs](http://docs.openstack.org/openstack-ops/content/floating_ips.html)
- [OpenStack hosted.meappy.com Dashboard](https://secuore.meappy.com/os/)

##### Basic Operations
###### Connecting to jump-host
1. SSH<br>
`[user@local-host ~] ssh -i user_key.pem -p 2233 user@jump-host.hosted.meappy.com`<br>

2. Source Keystone Identity file<br>
`[user@jump-host ~]$ source  keystonerc_user`<br>
`[user@jump-host ~(keystone_user)]$`<br>

###### OpenStack openrations after logging into jump-host
1. List Nova instances in project<br>
`[user@jump-host ~(keystone_user)]$ nova list`<br>
`+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`<br>
`| ID                                   | Name         | Status  | Task State | Power State | Networks                    |`<br>
`+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`<br>
`| 37d8cdf4-4079-4b23-acc6-8518c9b771eb | centos2      | SHUTOFF | -          | Shutdown    | int=192.168.1.4             |`<br>
`| 9cdec55e-a3c8-4c38-bdcb-7594eb3db3be | centos6      | ACTIVE  | -          | Running     | int=192.168.1.10, 10.1.1.67 |`<br>
`| 20736923-b1b4-4a49-898c-63fdc007d4d6 | centos6-2    | ACTIVE  | -          | Running     | int=192.168.1.11, 10.1.1.65 |`<br>
`| 2f5e5fca-4128-4a74-b6ec-d103b2b9e932 | instance5    | ACTIVE  | -          | Running     | int=192.168.1.9             |`<br>
`+--------------------------------------+--------------+---------+------------+-------------+-----------------------------+`<br>

2. List avaialble images<br>
`[user@jump-host ~(keystone_user)]$ glance image-list`<br>
`+--------------------------------------+------------------------------------------+-------------+------------------+------------+--------+`<br>
`| ID                                   | Name                                     | Disk Format | Container Format | Size       | Status |`<br>
`+--------------------------------------+------------------------------------------+-------------+------------------+------------+--------+`<br>
`| d618db8e-abd8-452c-8802-5b03a7425cf5 | CentOS-6-x86_64-GenericCloud-20141129_01 | qcow2       | bare             | 1151533056 | active |`<br>
`| 6cb73530-a737-4a22-853b-73a9f77a74e0 | CentOS-7-x86_64-GenericCloud-1503        | qcow2       | bare             | 1004994560 | active |`<br>
`| d6149b97-a006-46e5-9d2e-651fbbae0251 | CentOS-Atomic-Host-7-GenericCloud        | qcow2       | bare             | 916848640  | active |`<br>
`| 0c39fed9-2472-49c8-bda0-7af9673ec576 | centos6-snapshot                         | qcow2       | bare             | 1275789312 | active |`<br>
`| 60aa11ac-1841-4528-9295-6e244e3e3489 | CoreOS                                   | qcow2       | bare             | 493813760  | active |`<br>
`+--------------------------------------+------------------------------------------+-------------+------------------+------------+--------+`<br>

3. List keypairs<br>
`[user@jump-host ~(keystone_user)]$ nova keypair-list`<br>
`+----------+-------------------------------------------------+`<br>
`| Name     | Fingerprint                                     |`<br>
`+----------+-------------------------------------------------+`<br>
`| user_key | a8:89:4b:e6:15:1f:77:33:61:03:9d:fd:e4:a9:c4:9c |`<br>
`+----------+-------------------------------------------------+`<br>

4. List security groups<br>
`[user@jump-host ~(keystone_user)]$ nova secgroup-list `<br>
`+--------------------------------------+-----------+------------------------+`<br>
`| Id                                   | Name      | Description            |`<br>
`+--------------------------------------+-----------+------------------------+`<br>
`| 50973d6c-e2dd-496d-9811-57522f70311c | Web + SSH | Web + SSH              |`<br>
`| 2ed9ba36-42da-4dae-b073-d5caf323721d | default   | Default security group |`<br>
`+--------------------------------------+-----------+------------------------+`<br>

5. Launch instance<br>
`[user@jump-host ~(keystone_user)]$ nova boot --flavor m1-plus.tiny --key_name user_key --image d6149b97-a006-46e5-9d2e-651fbbae0251 --security-groups 'Web + SSH' instance1`<br>

6. Create floating IP<br>
`[user@jump-host ~(keystone_user)]$ nova floating-ip-create ext`<br>
`+--------------------------------------+-----------+-----------+----------+------+`<br>
`| Id                                   | IP        | Server Id | Fixed IP | Pool |`<br>
`+--------------------------------------+-----------+-----------+----------+------+`<br>
`| c4d13b92-8be9-455a-ba6a-eca5f804fe3c | 10.1.1.70 | -         | -        | ext  |`<br>
`+--------------------------------------+-----------+-----------+----------+------+`<br>

7. Attach floating IP to newly created instance<br>
`[user@jump-host ~(keystone_user)]$ nova floating-ip-associate instance1 10.1.1.70`<br>

8. SSH into instance from jump-host with private key file<br>
`[user@jump-host ~(keystone_user)]$ ssh -i .ssh/user_key.pem centos@10.1.1.70`<br>
`The authenticity of host '10.1.1.70 (10.1.1.70)' can't be established.`<br>
`ECDSA key fingerprint is 41:4a:f1:21:cb:e5:a6:62:92:f9:ea:6d:a6:7f:37:49.`<br>
`Are you sure you want to continue connecting (yes/no)? yes`<br>
`Warning: Permanently added '10.1.1.70' (ECDSA) to the list of known hosts.`<br>
`[centos@instance1 ~]$`<br>

9. SSH directly into instance from local machine, via jump-host<br>
`[user@local-host ~] ssh -i user_key1.pem -tt -p 2233 user@jump-host.hosted.meappy.com  ssh -i .ssh/user_key1.pem -tt centos@10.1.1.70`<br>
`[centos@instance1 ~]$`<br>
