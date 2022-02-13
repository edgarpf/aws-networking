# AWS Certified Advanced Networking - Specialty - Tips for certification exam
* Active session charge is not used for billing of the Network Address Translation (NAT) gateway.
* NAT gateway are highly available within single AZ. Hence for HA NAT gateway you must have NAT gateways in every AZ.
* Auto-assigned addresses are not eligible for recall. You can only recall Elastic IP addresses the account has owned. Tagging is not necessary. It is possible to recall Elastic IP addresses in some scenarios. The Elastic IP address is not related to an instance number because it won’t be automatically associated with an instance but rather returned to the account.
* Attaching an elastic network interface associated with a different subnet to an instance can make the instance dual-homed.
* The maximum allowable MTU of 1500 is available for traffic traversing via the Internet. If you are in a VPC , then you can use Jumbo frames to use more than that.
* EBS IOPS volumes should be used for database workloads.
* To send traffic from your instance to an instance in a peer VPC using private IPv4 addresses, you must add a route to the route table that's associated with the subnet in which the instance resides. The route points to the CIDR block (or portion of the CIDR block) of the other VPC in the VPC peering connection. The owner of the other VPC in the peering connection must also add a route to their subnet's route table to direct traffic back to your VPC. 
* You created a VPC with the CIDR block of 192.168.0.0./16. Instances were launched in the VPC. Now there is a decision to ensure the instances have an address space for 10.0.0.0/16. For that create a new VPC with the address block of 10.0.0.0/16. Create your instances in this new VPC.
* Since transitive peering is not allowed, you can use a proxy instance to forward the requests.   
* Ensure that the Instance is using Enhanced Networking for better network throughput.
* Cluster placement group can make low latency between the underlying instances that support the application.
* DPDK is the Data Plane Development Kit that consists of libraries to accelerate packet processing workloads running on a wide variety of CPU architectures. 
* The AWS Documentation clearly states that the most specific route in your route table that matches the traffic to determine how to route the traffic is used. Hence it is better to ensure the VPN connection has a less specific route to ensure that it is not the preferred route which is taken. The Direct Connect will be used.
* If the data needs to be encrypted end to end, use an SSL certificate which can be mapped to the application.
* Enable "DNSSupport" and "DNSHostnames" for the VPC to receive DNS hostnames in instances.
* There will be a data transfer charge of $0.01 per GB for instances in the same AZ in the same region via the Public IPs of the EC2 Instances.
* If there are overlapping CIDR blocks in two VPCs creation, the Cloud Formation template deployment will fail and all resources will be rolled back.
* The AWS Documentation mentions the following AWS Lambda runs your function code securely within a VPC by default. However, to enable your Lambda function to access resources inside your private VPC, you must provide additional VPC-specific configuration information that includes VPC subnet IDs and security group IDs. AWS Lambda uses this information to set up elastic network interfaces (ENIs) that enable your function to connect securely to other resources within your private VPC.
* To enable redundancy/high availability, each AWS Virtual Private Gateway (VGW) has two VPN endpoints with capabilities for static and dynamic routing. Although statically routed VPN connections from a single customer gateway are sufficient for establishing remote connectivity to a VPC, this is not a highly available configuration. The best practice for making VPN connections highly available is to use redundant customer gateways and dynamic routing for automatic failover between AWS and customer VPN endpoints.
* If you need to use a custom routing protocol instead of IPSec, the normal AWS VPN managed connections cannot be used. Instead, you have to decide on creating an EC2 instance and using a custom VPN software from the AWS Marketplace.
* AWS is only responsible for Ensuring the health of the underlying physical host of the EC2 Instance.
* To test that the VPN connection is working correctly, launch an instance into your VPC, and ensure that it does not have an Internet connection. After you've launched the instance, ping its private IP address from your Windows server. The VPN tunnel comes up when traffic is generated from the customer gateway, therefore the ping command also initiates the VPN connection.
* The clear requirements for setting up LAG group is given in the AWS Documentation The following rules apply: · All connections in the LAG must use the same bandwidth. The following bandwidths are supported: 1 Gbps and 10 Gbps. · You can have a maximum of 4 connections in a LAG. Each connection in the LAG counts towards your overall connection limit for the region. · All connections in the LAG must terminate at the same AWS Direct Connect endpoint.
* The AWS Direct Connect service now has a metric available in Cloudwatch called Connection State. You can design an alarm whenever the connection state is DOWN.
* Following are the requirements given in the AWS Documentation for AWS Direct Connect 
  * · Your network must use single mode fiber with a 1000BASE-LX (1310nm) transceiver for 1 gigabit Ethernet, or a 10GBASE-LR (1310nm) transceiver for 10 gigabit Ethernet. 
  * · Auto-negotiation for the port must be disabled. Port speed and full-duplex mode must be configured manually. 
  * · 802.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices. 
  * · Your device must support Border Gateway Protocol (BGP) and BGP MD5 authentication.
* In AWS Direct Connect you pay for the port hours and data transfer out (than includes for example data transfer from S3 via a public VIF and data transfer from VPC via a private VIF).
* Bidirectional Forwarding Detection (BFD) is a network fault detection protocol that provides fast failure detection times, which facilitates faster re-convergence time for dynamic routing protocols. It is independent of media, routing protocol, and data. We recommend enabling BFD when configuring multiple AWS Direct Connect connections or when configuring a single AWS Direct Connect connection and a VPN connection as a back up to ensure fast detection and failover.
* In a route table static route has priorit over a propagated route.
* Simple AD forwards DNS requests to the IP address of the Amazon-provided DNS servers for your VPC. These DNS servers will resolve names configured in your Route 53 private hosted zones. By pointing your on-premises computers to your Simple AD, you can now resolve DNS requests to the private hosted zone. 
* In the edge location, CloudFront checks its cache for the requested files. If the files are in the cache, CloudFront returns them to the user. If the files are not in the cache, it does the following: a. CloudFront compares the request with the specifications in your distribution and forwards the request for the files to the applicable origin server for the corresponding file type—for example, to your Amazon S3 bucket for image files and to your HTTP server for the HTML files. b. The origin servers send the files back to the CloudFront edge location. c. As soon as the first byte arrives from the origin, CloudFront begins to forward the files to the user. CloudFront also adds the files to the cache in the edge location for the next time someone requests those files.
* While ordinary Amazon Route 53 records are standard DNS records, alias records provide a Route 53–specific extension to DNS functionality. Instead of an IP address or a domain name, an alias record contains a pointer to a CloudFront distribution, an Elastic Beanstalk environment, an ELB Classic, Application, or Network Load Balancer, an Amazon S3 bucket that is configured as a static website, or another Route 53 record in the same hosted zone.
* If you want to ensure that the minimal number of packets can be sent across the network interfaces. Change the MTU setting on the network interface for each instance.
* Imagine you have two on-premise data centers (DataCenter 1/2) If you want that, in the event the primary connection to DataCenter1 goes down, traffic should be directed to Data Center2 you need:
  * Make use of AS-PATH prepending.
  * Ensure DataCenter2 advertises less specific routes.
* Enhanced Networking Enhanced networking uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types. 
* To connect to your WorkSpaces, the network that your Amazon WorkSpaces clients are connected to must have certain ports open to the IP address ranges for the various AWS services (grouped in subsets). These address ranges vary by AWS region. These same ports must also be open on any firewall running on the client.
* You can use a VPN or a seconde Direct Connection as a backup for a primary DC.
* If you try to add more instances to the placement group later, or if you try to launch more than one instance type in the placement group, you increase your chances of getting an insufficient capacity error.
* When you use Amazon Redshift Enhanced VPC Routing, Amazon Redshift forces all COPY and UNLOAD traffic between your cluster and your data repositories through your Amazon VPC.
* If you need to sniff the actual network packets of a EC2 application, the ideal approach would be to use a network monitoring tool provided by an AWS partner. 
* You have an on-premise application that needs access to the Simple Storage Service. Some of the key requirements are high bandwidth for the connection, low jitter and high availability. For that you should use AWS Direct Connect with public VIF.
* Make use of VPC peering and Consider a Hub and Spoke Model VPC Design if you want to host an Active Directory Domain server in a VPC. Resources in other VPCs will need to access the domain server for authentication and DNS routing.
* You can attach 2 ENI’s to the Instance. One ENI can be used to accept Internet traffic and the other can be used to interact with your instances in the private subnet. 
* All data transfer into AWS via the Internet is not charged.
* AWS uses the most specific route in your route table that matches the traffic to determine how to route the traffic (longest prefix match).