# API Consul Examples

Build upon the DNS Example, but use the Consul API to query instead of DNS.

## API Example

### Notes

Requirements:

* [Setup DNS Example](../02-dns/README.md)


### Connect Local Consul client to Consul instance

Session 1 (Host):

```bash
# pickup were left off from DNS example

# remind us of CONSUL's IP address
cat $CONSUL_HTTP_ADDR

# list all members of cluster
curl $CONSUL_HTTP_ADDR/v1/agent/members

# list all services
curl $CONSUL_HTTP_ADDR/v1/agent/services
```
