# Consul Learning

## Installation

### Mac

```bash
# Install consul for CLI access from host
brew install consul

# Test version of consul
consul version

# Running local examples using Ubuntu VMs
brew install multipass

# test version of multipass
multipass version

```

### Common Multipass Commands

Local consul examples use Multipass to manage local VMs.

```bash
# Find all Ubuntu images
multipass find

# Create running instance, instance/vm name can be used by other commands later on
multipass launch -name <name> [other-options] <image-name>

# Get VM instance information (IP address, etc)
multipass info <name>

# Show all instances
multipass list

# Access terminal session within running instance
multipass shell <name>

# Stop running instance to save on resources
multipass stop <name>

# Start a stopped instance
multipass start <name>

# Stop and then start instance again
multipass restart <name>

# Delete/destroy instance
multipass delete <name>

# Purge deleted instances
multipass purge
```

## Examples

* [Simple Example](examples/01-simple/README.md) - just get Consul up and running
* [DNS Example](examples/02-dns/README.md) - Use standard DNS to resolve service names
