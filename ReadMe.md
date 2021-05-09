This is a single node kubernetes cluster set up using Vagrant and Ansible.
Vagrant uses an Ubuntu-Bionic image and Shell and Ansible-Local as provisioners.

An arbitraty IP of 192.168.47.1 is chosen for the guest VM, as well as 10.244.0.0/16 as CIDR for pod network.

This solution uses Weave as container network provider and Docker as CRI.




