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

```sh
https://github.com/openshift/openshift-ansible
cd openshift-ansible
bin/cluster create aws mycluster
```



