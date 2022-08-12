# DNS Consul Examples

## DNS Example

### Notes

Requirements:

* Consul installed on host for CLI access
* Multipass installed for running VMs

Easiest with multiple sessions.

### Create Consul Instance

Session 1 (Host):

```bash
# Create consul-dev instance
multipass launch --name consul-dev --cloud-init https://raw.githubusercontent.com/jgt-contino/consul-learning/main/setup/multipass/consul-dns.yaml jammy
```

### Run Consul on Instance

Session 2 (Server):

```bash
# Login to consul-dev instance
multipass shell consul-dev

# Start Consul in Dev mode, listen on all IPs (must run as root for DNS):
sudo consul agent -dev -client 0.0.0.0 -dns-port 53

# Once consul is running - no additional commands will be given here - instead, this is for monitoring consul server messages
```

### Connect Local Consul client to Consul instance

Session 1 (Host):

```bash
# Find IP of instance:
multipass info consul-dev
# or can use multipass list
# Make note of IPv4 address

# Open web browser on host to:
#  http://<IPADDR>:8500/

# set consul http address for CLI

export CONSUL_IP=<IPADDR>
export CONSUL_HTTP_ADDR=${CONSUL_IP}:8500

# Get consul info
consul info

# List "members" of consul cluster
consul members
```

### Register Services

```bash
# register services
consul services register -name web -address "192.168.64.10" -port 80

consul services register -name database -address "192.168.64.12" -port 3600

consul catalog services
```

### Query DNS for Services

```bash
# double check IP env is set
cat $CONSUL_IP

# query for web address
dig @$CONSUL_IP web.service.consul

# query for database, with port
dig @$CONSUL_IP database.service.consul -t SRV
```
