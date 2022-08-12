# Simple (Dev-mode) Consul Examples

## Simple Example

### Notes

Requirements:

* Consul installed on host for CLI access
* Multipass installed for running VMs

Easiest with multiple sessions.

### Create Consul Instance

Session 1 (Host):

```bash
# Create consul-dev instance
multipass launch --name consul-dev --cloud-init https://raw.githubusercontent.com/jgt-contino/consul-learning/main/simple/consul.yaml jammy
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
# Make note of IPv4 address

# Open web browser on host to:
#  http://<IPADDR>:8500/

# set consul http address for CLI
export CONSUL_HTTP_ADDR=<IPADDR>:8500

# Get consul info
consul info

# List "members" of consul cluster
consul members
```

### Register a Service

```bash
# register a "service"
consul services register -name web
```
