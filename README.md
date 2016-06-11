##  Initial setup

> Ansible & auth keys setup 

```sh
ssh-agent $SHELL
ssh-add you_aws_key.pem
export PYTHONPATH=/opt/ansible/ansible/lib
export ANSIBLE_LIBRARY=/opt/ansible/ansible/library
export PATH=/opt/ansible/ansible/bin:/bin:/usr/bin:/sbin:/usr/sbin
```

> change .aws_creds     

```sh
source .aws_creds
```

> Change the ssh-user in aws config  

```sh
vi playbooks/aws/openshift-cluster/vars.yml
#ssh_user: centos
```

## Run Openshift Cluster installation

> Clone repo and invoke install  

```sh
https://github.com/openshift/openshift-ansible
cd openshift-ansible
bin/cluster create aws mycluster
```
> Install Registry  

```sh
ssh centos@masterip
sudo docker ps 
sudo docker exec -it  masterpod_id sh

oadm registry --config=/etc/origin/master/admin.kubeconfig \
    --credentials=/etc/origin/master/openshift-registry.kubeconfig \
    --images='registry.access.redhat.com/openshift3/ose-${component}:${version}' 

# replace *origin* with *openshift*  in case of enterprise installation

```


    


