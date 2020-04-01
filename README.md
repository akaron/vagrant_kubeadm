For test only. Provision 3 virtual machines using Vagarnt and deploy kubernetes on
these machines use ansible + kubeadm.

This repo is simplified version of
https://github.com/geerlingguy/ansible-for-kubernetes/tree/master/cluster-local-vms .
Here removes the use of roles from ansible-galaxy, supports only Debian 10 so no need
the os-specific condition/variable/tasks, and remove some variables.

To run it, only need `vagrant up`. It brings up 3 nodes, and run the playbook
`main.yml`. Then run `ansible-playbook -i inventory test-deployment.yml` for a test
deployment. 

# notes
* There are still ansible-galaxy roles `gerrlingguy.security` in
  `requirements.yml`.  It is probably no need to worry about security for test
  purpose.  If want to try it, run `ansible-galaxy install -r requirements.yml` to
  install the role and uncomment the role in `main.yml` to use it.
* system requirement: it creates three machines with 2G of RAM each. It's too much
  for my macbook pro which has intel i5 2.3GHz dual core and 8G ram. Running it on
  the macbook cause it quite unstable and freeze or reboot frequently.


