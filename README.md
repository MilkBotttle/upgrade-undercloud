# Backup undercloud
Check [backup-undercloud](https://github.com/MilkBotttle/backup-undercloud)
# Upgrade UC P -> Q
1. Update repo version to queens
Create queens repo manually for offline environment or install with network:
```
yum localinstall -y $(curl -L --silent https://trunk.rdoproject.org/centos7/current | grep python2-tripleo-repos | awk -F "href" {'print $2'} | awk -F '"' {'pr
int $2'})
tripleo-repos -b queens current ceph
```
There is a bug ceph repository `tripleo-centos-ceph-jewel.repo` use baseurl `baseurl=None/centos/7/storage/x86_64/ceph-jewel/` need fix to `baseurl=http://mirr
or.centos.org/centos/7/storage/x86_64/ceph-jewel/`

2. Update tripleo package
```
sudo yum update python-tripleoclient* openstack-tripleo-common openstack-tripleo-heat-templates
```
3. Upgrade undercloud
```
openstack undercloud upgrade
```
4. Upload new overclud image for feature replace or scale.
If you want to upgrade to rocky ignore this.
```
openstack overcloud image upload --update-existing
```

# upgrade-undercloud
