For test only. Provision 3 virtual machines using Vagarnt and deploy kubernetes on
these machines use ansible + kubeadm.

This repo is simplified version of
https://github.com/geerlingguy/ansible-for-kubernetes/tree/master/cluster-local-vms .
Here removes the use of roles from ansible-galaxy, supports only Debian 10 so no need
the os-specific condition/variable/tasks, and remove some variables.

# steps
All commands running on host machine, inside the folder.

* Run `vagrant up`
    - brings up 3 nodes, and run the playbook `main.yml`
* Run `ansible-playbook -i inventory test-deployment.yml`
    - deploy the deployment https://hub.docker.com/r/paulbouwer/hello-kubernetes
* open browser to verify the deployment
    - run `ansible kube1 -i inventory -m shell -b -a "kubectl get svc -o wide"`
      to get the `NodePort`
    - open browser and open page `http://192.168.7.3:32752`. Change the `32752`
      to the `NodePort` above.

# notes
* There are still ansible-galaxy roles `gerrlingguy.security` in
  `requirements.yml`.  It is probably no need to worry about security for test
  purpose.  If want to try it, run `ansible-galaxy install -r requirements.yml` to
  install the role and uncomment the role in `main.yml` to use it.
* system requirement: it creates three machines with 2G of RAM each. It's too much
  for my macbook pro which has intel i5 2.3GHz dual core and 8G ram. Running it on
  the macbook cause it quite unstable and freeze or reboot frequently.


