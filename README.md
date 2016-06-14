> *Background*:  This Repo covers installing openshift origin (enterprise may work too) on Atomic host  
> Installing openshift on atomic host is no different, only thing to remember is openshift is installed as containers running on master/nodes not as rpms.   and other step is to choose Atomic host aws ami as your host image.  that's all


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



## Run Openshift Cluster installation

> Clone repo and invoke install  

```sh
git clone https://github.com/openshift/openshift-ansible
cd openshift-ansible
```
> Change the ssh-user in aws config  

```sh
vi playbooks/aws/openshift-cluster/vars.yml
#ssh_user: centos
vi ./playbooks/byo/rhel_subscribe.yml  & vi ./playbooks/common/openshift-cluster/update_repos_and_packages.yml
#- os_update_latest    -- comment out this entry
```
> Run the cluster installation 

```sh
bin/cluster create aws --deployment-type=origin mycluster
# if the install fails re-run with update
bin/cluster update aws --deployment-type=origin  mycluster

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


    


