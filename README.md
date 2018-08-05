# Ansible for Docker Swarm/Kubernetes cluster

It is a collection of ansible roles to provision Docker Swarm and
Kubernetes cluster for development environment. It is NOT recommended to use it
AS IS for production environment.

## Setup

### Docker Swarm cluster

Edit inventories/cluster-swarm.yml:
- In docker-manager section, adds manager/IP address;
- In docker-worker section, adds workers name/IP addresses (one per line)

If manager has multiple network interfaces, edit group_vars/docker-manager file
and replace mgr_iface by the network interface name (for example eth1, br0...).

Choosing specific network interfaces is also available for workers by editing
group_vars/docker-worker file.

### Kubernetes cluster
                                                                                
Edit inventories/cluster-kubernetes.yml:                                                   
- In kubernetes-master section, adds master/IP address;                           
- In kubernetes-worker section, adds workers name/IP addresses (one per line)       

## Deployment

Use classic `ansible-playbook` command.

### Docker Swarm cluster

```
ansible-playbook -i ./inventories/cluster-swarm.yml ./playbook.yml -u user 
```

Be sure to replace `user` with your own. This account must have sudo rights.

To verify if it is OK after deployment, run `docker node ls` on the manager
and check if you see all manager and worker nodes in ready state.

### Kubernetes cluster

```
ansible-playbook -i ./inventories/cluster-kubernetes.yml ./playbook.yml -u user 
```

Be sure to replace `user` with your own. This account must have sudo rights.

To verify if it is OK after deployment, run `kubectl get nodes` on the master
and check if you see all manager and worker nodes in ready state.

## Limitations

For the moment in either Docker Swarm or Kubernetes role:

 * Only one manager/master can be configured;
 * Nodes are configured to connect only via IPv4;
 * Kubernetes role has some Debian specific stuff and so works only for 
 Debian-like distributions.

These limitations may be fixed one day!

## Links

 * https://www.docker.com/
 * https://docs.docker.com/engine/swarm/
 * https://www.kubernetes.io

