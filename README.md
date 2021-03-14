
## Serving HTTP requests to 200 subnets

201 VMs were placed on 201 different subnets (10.0.x.0/24, where
x=1..201).  Each of the first 200 VMs generated one HTTP request every
2 seconds.  These requests were served by a HTTP server running in
the subnet at http://10.0.201.1.  The file `http-from-200-subnets.pcap.gz`
contains 60 seconds of packet data captured on the interface of the
HTTP server VM that connected to the router.  All 201 VMs and router
were deployed from LiquidMetal template.

## Random connections on clusters of 250 virtual machines

The 200 files `subnet-001.pcap.gz` through `subnet-200.pcap.gz` each
contains 60 seconds of pcap packet data from a different cluster of
250 virtual machines.  The first cluster of machines were all on the
10.0.1.0/24 subnet, the second cluster on the 10.0.2.0/24 subnet, and
so forth. Each virtual machine sent TCP requests once per second to
another randomly selected virtual machine in the cluster.  Also once
per second, each virtual machine sent one IMCP ping request to a
randomly selected virtual machine.  Each cluster was deployed
one-at-a-time to a LiquidMetal environment from a template.  After
pcap data was collected, the environment was destroyed before
deploying the next template.
