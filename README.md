
## Serving HTTP requests to 200 subnets

201 VMs were placed on 201 different subnets (10.0.x.0/24, where
x=1..201).  Each of the first 200 VMs generated one HTTP request every
2 seconds.  These requests were served by a HTTP server running in
the subnet at http://10.0.201.1.  The file `http-from-200-subnets.pcap.gz`
contains 60 seconds of packet data captured on the interface of the
HTTP server VM that connected to the router.  All 201 VMs and router
were deployed from LiquidMetal template.

The following steps can be used to repeat the data capture:

  1. Launch the template named "router-with-201-subnets" into the LiquidMetal editor
     - Note: starting the editor with so many components sometimes will
       make the browser report that the web page is not responsive.
       After some time, possibly many minutes, these messages will stop
       appearing and the web browser will become responsive again.

  2. After the editor shows the 201 VMs (on different subnets) and the
     router and becomes responsive, click once on the `DEPLOY` button.
     Choose a name like `router-test` when the `Deployments` dialog
     appears.
     - Note: deploying the 201 components will take about 2 minutes.

  3. After the `LIVE` menu becomes active, select the name you chose
     from the menu.
     - Note: like before, the browser may become unresponsive for many
       minutes.  Please wait until it becomes responsive again.

  4. It is possible to capture pcap data using the LiquidMetal GUI,
     however because of new feature development.  However, for this
     particular demo, it is currently better to capture pcap data from
     the command line.  As a first step, right click on the ROUTER
     icon and select the console feature.

  5. All network traffic to the web server goes through the interface
     named `eth200`.  To record 60 seconds of pcap data, type the
     following command into the console:

```
tcpdump -i eth200 -G 60 -W 1 -w http.pcap
```

  6. After the `tcpdump` command completes, you can download the file
     by right clicking on the ROUTER icon and selecting `Files`.  It should
     be possible to find the new pcap file and download it by double
     clicking on it.

  7. When finished, destroy the environment by clicking on the `DESTROY` button.


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
