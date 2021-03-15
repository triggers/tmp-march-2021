
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
     Type in a name like `router-test` when the `Deployments` dialog
     appears.
     - Note: deploying the 201 components will take about 2 minutes.

  3. After the `LIVE` menu becomes active, select the name you chose
     from the menu.
     - Note: like before, the browser may become unresponsive for many
       minutes.  Please wait until it becomes responsive again.

  4. It is possible to capture pcap data using the LiquidMetal GUI.
     However, because of new feature development, for this
     particular demo it is currently better to capture pcap data from
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
per second, each virtual machine sent one ICMP ping request to a
randomly selected virtual machine.  Each cluster was deployed
one-at-a-time to a LiquidMetal environment from a template.  After
pcap data was collected, the environment was destroyed before
deploying the next template.

The following steps can be used to repeat the data capture for one of
the pcap files:

  1. Launch one of the templates with a name like "subnet-003" into
     the LiquidMetal editor

  2. Click once on the `DEPLOY` button.  Type in a name like
     `cluster-test` when the `Deployments` dialog appears.
     - Note: deploying the 250 cluster nodes will take about 2 minutes.

  3. After the `LIVE` menu becomes active, select from the menu the name that you typed in.

  4. For pcap data capture on a cluster, the LiquidMetal GUI can be
     used.  Right click on the ROUTER icon and select the `Packet Capture`
     feature.

  5. On the "Packet Request" dialog, select `eth0` as the "Interface
     to Read"

  6. To capture 60 seconds of pcap data, enter `0` for the "# of Pkts"
     and `60000` for "Time Limit (ms)".  Also select the "File Only"
     checkbox to prevent the thousands of packets from trying to
     display in the UI.

  7. To start the capture, click on the `CAPTURE PACKETS` button.  The
     UI will animate while the capture is taking place.

  8. After a little more than 60 seconds, the animation should stop
     and a new download button will appear as a cloud icon with a
     downward pointing arrow.  Click on this button and the new pcap
     file will download.

  9. When finished, destroy the environment by clicking on the `DESTROY` button.

