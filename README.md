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
* You can use a VPN or a second Direct Connection as a backup for a primary DC.
* If you try to add more instances to the placement group later, or if you try to launch more than one instance type in the placement group, you increase your chances of getting an insufficient capacity error.
* When you use Amazon Redshift Enhanced VPC Routing, Amazon Redshift forces all COPY and UNLOAD traffic between your cluster and your data repositories through your Amazon VPC.
* If you need to sniff the actual network packets of a EC2 application, the ideal approach would be to use a network monitoring tool provided by an AWS partner. 
* You have an on-premise application that needs access to the S3. Some of the key requirements are high bandwidth for the connection, low jitter and high availability. For that you should use AWS Direct Connect with public VIF.
* Make use of VPC peering and Consider a Hub and Spoke Model VPC Design if you want to host an Active Directory Domain server in a VPC. Resources in other VPCs will need to access the domain server for authentication and DNS routing.
* You can attach 2 ENI’s to the Instance. One ENI can be used to accept Internet traffic and the other can be used to interact with your instances in the private subnet. 
* All data transfer into AWS via the Internet is not charged.
* AWS uses the most specific route in your route table that matches the traffic to determine how to route the traffic (longest prefix match).
* You need to use a VPN IPSec tunnel for secure communication across the Internet between the regions.
* The data transfer charges AWS Direct Connect data transfer Data transfer IN is $0.00 per GB in all locations. Data Transfer OUT pricing is dependent on the source AWS Region and AWS Direct Connect location.
* Use the same Public VIF from your current AWS Direct connect connection to use AWS Direct connect between regions.
* You can create a Direct Connect gateway in any region and use it to connect your AWS Direct Connect connection over a private virtual interface to VPCs in your account that are located in different regions. Alternatively, you can create a public virtual interface for your AWS Direct Connect connection and then establish a VPN connection to your VPC in the remote region.
* What you need to use Connect Direct:
  * ![alt text](https://i.ibb.co/XttsgzZ/image.png)
* If your Lambda function requires Internet access (for example, to access AWS services that don't have VPC endpoints ), you can configure a NAT instance inside your VPC or you can use the Amazon VPC NAT gateway.
* Enhanced networking uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types. Enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. Also when it comes to setting the MTU , you can enable Jumbo frames by setting the MTU to 9001.
* The maximum that is allowable in VPC peering is MTU 1500 For placement groups to work. 
* the configuration for the Distribution in such a scenario Origin Protocol Policy Change the Origin Protocol Policy for the applicable origins in your distribution: HTTPS Only – CloudFront uses only HTTPS to communicate with your custom origin. Match Viewer – CloudFront communicates with your custom origin using HTTP or HTTPS, depending on the protocol of the viewer request. For example, if you choose Match Viewer for Origin Protocol Policy and the viewer uses HTTPS to request an object from CloudFront, CloudFront also uses HTTPS to forward the request to your origin.
* VLAN ID and the Virtual Private gateway is part of the AWS Direct Connect connection creation process.
* For RTMP distributions, you cannot configure CloudFront to forward query string parameters to your origin. 
* When you create a workspace, you need to choose an existing User Directory.
* After you have downloaded your Letter of Authorization and Connecting Facility Assignment (LOA-CFA), you need to complete your cross-network connection, also known as a cross connect. If you already have equipment located in an AWS Direct Connect location, contact the appropriate provider to complete the cross connect.
* When troubleshooting AWS Direct Connect , one of the key issues is to ensure that the number of IP Prefixes summarised is below 100. Hence one of the steps would be to ensure that the routes are summarised into a default route.
* AWS Inspector have the "Network Reachibility" rules package which help in running network port-scanning tools to test routing and firewall configurations and then validate what processes are listening on your instance network ports, before finally mapping the IPs identified in the port scan back to the host’s owner.
* You can create a new DHCP options set and then provide the NTP server name as part of the options set if The EC2 Instances hosted in the VPC needs to get the time from a custom NTP server. 
* When the instances are getting terminated by Autoscaling, the requests can be partially fulfilled and not completed. In such a case you can increase the connection draining on the ELB.
* Do not routes advertise many routes on from On-premise in AWS Direct Connect.
* You can resolve domain names in private hosted zones from your on-premises network by configuring a DNS forwarder. Setup a DNS forwarder in your VPC. Ensure the DNS forwarder points to the Amazon DNS resolver for the VPC. Also ensure the forwarder is configured with the on-premise DNS server. Change the Option Set for the VPC for the IP address of the DNS forwarder. Configure a DNS forwarder in the On-premise location.
* You can provide secure communication between sites using the AWS VPN CloudHub.
* For the Site office, you can use AWS Site-to-Site VPN. Since there is no mechanism currently for point to site connectivity for individual devices, you need to use a custom VPN server.
* If the requirements are very specific you will need to use a custom VPN from the AWS Marketplace.
* you can ensure that the CloudHSM modules are scaled along with the EC2 Instances for ensuring on time delivery of the SSL certificates by specifing the nmber of HDM modules in the cluster.
* You have a requirement to host an application in the VPC which primarily communicates on IPv6. EnableIPv6 in VPC and subnets.
* NAT Gateway Doesn't Respond to a Ping Command If you try to ping a NAT gateway's Elastic IP address or private IP address from the internet.
* Support this Attaching multiple network interfaces to an instance is useful when you want to: 
  * Create a management network. 
  * Use network and security appliances in your VPC. 
  * Create dual-homed instances with workloads/roles on distinct subnets. 
  * Create a low-budget, high-availability solution. 
* The Flow Logs will not include any of the following traffic: 
  * Traffic to Amazon DNS servers, including queries for private hosted zones. 
  * Windows license activation traffic for licenses provided by Amazon. 
  * Requests for instance metadata. 
  * DHCP requests or responses. 
* To perform load testing that accurately assesses CloudFront performance, we recommend that you do all of the following: 
  * Send client requests from multiple geographic regions. 
  * Configure your test so each client makes an independent DNS request; each client will then receive a different set of IP addresses from DNS. 
  * For each client that is making requests, spread your client requests across the set of IP addresses that are returned by DNS, which ensures that the load is distributed across multiple servers in a CloudFront edge location.
* You can configure Amazon Route 53 to log information about the queries that Route 53 receives, such as the following: 
  * The domain or subdomain that was requested 
  * The date and time of the request 
  * The DNS record type (such as A or AAAA) 
  * The Route 53 edge location that responded to the DNS query 
  * The DNS response code, such as NoError or ServFail
* An endpoint service supports IPv4 traffic over TCP only.
* Amazon GuardDuty is a managed threat detection service that continuously monitors for malicious or unauthorized behavior to help you protect your AWS accounts and workloads.
* You can attach a network interface in one subnet to an instance in another subnet in the same VPC; however, both the network interface and the instance must reside in the same Availability Zone.
* Hosted virtual interfaces (VIF) can connect to public resources or a VPC in the same way as standard VIFs, except that the account that owns the hosted VIF is different from the connection owner. Bandwidth is shared across all virtual interfaces on the parent connection. Hosted connections allow an APN partner to create a Direct Connect sub-1G connection for you, allocating dedicated bandwidth for that connection rather than having multiple VIFs on the same parent connection competing for bandwidth.
* Currently Amazon VPC service doesn’t presently permit multicast or broadcast traffic. In the event that you have an application that uses multicast to function, you can leverage GRE tunnels to create a mesh VPN overlay network between your Amazon EC2 instances.
* You need to disable Source/Dest checking on your EC2 instance to use VPN software on an EC2 Instance.
* With One Virtual Private gateway Two AWS Direct Connect Locations Two Customer gateways you can achieve maximum fault tolerance , have maximum bandwidth at all times.
* Setup a simple AD and make your on-premises severs points to the simple AD.
* Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record.
*  Jumbo frames allow more than 1500 bytes of data by increasing the payload size per packet, and thus increasing the percentage of the packet that is not packet overhead. Fewer packets are needed to send the same amount of usable data. However, outside of a given AWS region (EC2-Classic), a single VPC, or a VPC peering connection, you will experience a maximum path of 1500 MTU. VPN connections and traffic sent over an Internet gateway are limited to 1500 MTU. If packets are over 1500 bytes, they are fragmented, or they are dropped if the Don't Fragment flag is set in the IP header.
* IPv6 addresses are globally unique, and are therefore public by default. If you want your instance to be able to access the Internet, but you want to prevent resources on the Internet from initiating communication with your instance, you can use an egress-only Internet gateway.
* If you have a Direct Connect connection and also have a VPN as a backup connection ensure that prefixes are advertised the same on both connections.
* Simple AD does not require much management work.
* You can create your own EC2 Instance which will act as the DNS server. The VPC can then use the DHCP Options which points to this EC2 Instance as the DNS resolver.
* Attach a secondary ENI to the Instance to create a standby interface in case of any of the EC2 instances not responding to traffic.
* Virtual Routing and Forwarding (VRF) is a technology that allows multiple instances of a routing table to co-exist within the same router at the same time. Because the routing instances are independent, the same or overlapping IP addresses can be used without conflicting with each other. 
* In order to communicate with a DNS Server , the instance needs to reach the DNS server on port 53 for both TCP and UDP.
* You can use an Intrusion Detection system to do a packet level analysis.
* Each Amazon Route 53 hosted zone is associated with four name servers, known collectively as a delegation set. By default, the name servers have names like ns-2048.awsdns-64.com. If you want the domain name of your name servers to be the same as the domain name of your hosted zone, for example, ns1.example.com, you can configure white label name servers, also known as vanity name servers or private name servers. To create a reusable delegation set, you can use the Route 53 API, the AWS CLI, or one of the AWS SDKs.
* You will only get charged for the data transfer out in AWS Direct Connection.
* CIDR blocks for IPv4 and IPv6 are treated separately. For example, a route with a destination CIDR of 0.0.0.0/0 (all IPv4 addresses) does not automatically include all IPv6 addresses. You must create a route with a destination CIDR of ::/0 for all IPv6 addresses.
* When configuring Active Passive configuration for your VPN connections you should use AS_PATH prepending and more specific routes. 
*  AWS will always prefer to send traffic over an AWS Direct Connect connection, so no additional configuration is required to define primary and backup connections.
* You are charged for each "VPN Connection-hour" that your VPN connection is provisioned and available. Each partial VPN Connection-hour consumed is billed as a full hour.
* When configuring a Public VIF for AWS Direct Connect VPG is not necessary.
* Your company currently has VPC’s located in us-west and us-east. The company has an AWS Direct Connect connection in the US East region. They want to have the ability to extend the connection to us-west. They also need to minimize time and effort to have this in place. For that you can use Direct Connect Gateway.
* If the IP of the Application Load balancer keeps on changing, the workaround is to have a Network Load balancer in front of the ALB. An elastic IP is then assigned to the Network Load balancer and in this way the IP address wont change. 
* You can execute a Lambda function at an Amazon CloudFront Edge Location. This capability enables intelligent processing of HTTP requests at locations that are close (for the purposes of latency) to your customers.
*  An IP access control group acts as a virtual firewall that controls the IP addresses from which users are allowed to access their WorkSpaces. 
* An interface VPC endpoint (AWS PrivateLink) enables you to connect to services powered by AWS PrivateLink. These services include some AWS services, services hosted by other AWS accounts (referred to as endpoint services), and supported AWS Marketplace partner services. 
* AWS now supports Client-to-site VPN.
* BGP Communities AWS Direct Connect supports a range of BGP community tags to help control the scope (regional or global) and route preference of traffic. Scope BGP Communities You can apply BGP community tags on the public prefixes you advertise to Amazon to indicate how far to propagate your prefixes in the Amazon network.
* Use the customer gateway on your side to route traffic through the VPN tunnel.
* If you requested a sub-1G connection from your selected partner, they create a hosted connection for you (you cannot create it yourself. You must accept it in the AWS Direct Connect console before you can create a virtual interface.
* A VPN that connects your office to your Amazon VPC over an AWS Direct Connect connection is likely to be faster and more secure than a VPN that connects to your VPC over the internet. Create an AWS Direct Connect connection. Configure a public virtual interface for the Direct Connect connection.
* A requester-managed network interface is a network interface that an AWS service creates in your VPC. This network interface can represent an instance for another service, such as an Amazon RDS instance, or it can enable you to access another service or resource, such as an AWS PrivateLink service, or an Amazon ECS task. You cannot modify or detach a requester-managed network interface. If you delete the resource that the network interface represents, the AWS service detaches and deletes the network interface for you.
* In addition to VPC peering and setting the right route tables , the security groups for the AD EC2 instance needs to ensure the right rules are put in place for allowing incoming traffic.
* Configure the VPN connection in an Active/Passive configuration and advertise a more specific prefix for tunnel A if A is preferred over tunnel B when sending traffic from AWS to the on-premises network.
* Set up a public virtual interface on the Direct Connect connection. Create an AWS Site-to-Site VPN between the customer gateway and the virtual private gateway in the VPC if an application running on an EC2 instance in the VPC needs to access customer data stored in the on-premises data center with consistent performance.
* Create four private VIFs, that is, one VIF each from the on-premises data center to each of the VPCs. Enable VPC peering between all VPCs if you have 4 enviroments that need to communicade with each other.
* There are two types of Direct Connect connections:
  * Dedicated Connection: A physical Ethernet connection associated with a single customer. Customers can request a dedicated connection through the AWS Direct Connect console, the CLI, or the API.
  * Hosted Connection: A physical Ethernet connection that an AWS Direct Connect Partner provisions on behalf of a customer. Customers request a hosted connection by contacting a partner in the AWS Direct Connect Partner Program, which provisions the connection.
* Longest prefix match, Static routes, Direct-Connect BGP routes, VPN BGP routes from the MOST preferred to the LEAST preferred.
* If propagated routes from a Site-to-Site VPN connection or AWS Direct Connect connection overlap with the local route for your VPC, the local route is most preferred even if the propagated routes are more specific.
* When using Direct Connect to transport production workloads between AWS services, it's a best practice to create two connections through different data centers or providers. You have two options on how to configure your connections:
  * Active/Active – Traffic is load-shared between interfaces based on flow. If one connection becomes unavailable, all traffic is routed through the other connection.
  * Active/Passive – One connection handles traffic, and the other is on standby. If the active connection becomes unavailable, all traffic is routed through the passive connection.
* Allow your customer gateway to advertise the same prefix (public IP or network that you own) with the same Border Gateway Protocol (BGP) attributes on both public virtual interfaces. This configuration permits you to load balance traffic over both public virtual interfaces.
* Amazon VPC provides network routing flexibility. This includes the ability to create secure VPN tunnels between two or more software VPN appliances to connect multiple VPCs into a larger virtual private network so that instances in each VPC can seamlessly connect using private IP addresses. This option is recommended when you want to manage both ends of the VPN connection using your preferred VPN software provider.
* Records without a health check are always considered healthy. If no record is healthy, all records are deemed to be healthy.
* If you're creating failover records in a private hosted zone, you must assign a public IP address to an instance in the VPC to check the health of an endpoint within a VPC by IP address.
* If propagated routes from a Site-to-Site VPN connection or AWS Direct Connect connection have the same destination CIDR block as other existing static routes (longest prefix match cannot be applied), AWS prioritizes the static routes whose targets are an internet gateway, a virtual private gateway, a network interface, an instance ID, a VPC peering connection, a NAT gateway, a transit gateway, or a gateway VPC endpoint.
* To resolve any DNS queries for resources in the AWS VPC from the on-premises network, you can create an inbound endpoint on Route 53 Resolver and then DNS resolvers on the on-premises network can forward DNS queries to Route 53 Resolver via this endpoint.
* To resolve DNS queries for any resources in the on-premises network from the AWS VPC, you can create an outbound endpoint on Route 53 Resolver and then Route 53 Resolver can conditionally forward queries to resolvers on the on-premises network via this endpoint. To conditionally forward queries, you need to create Resolver rules that specify the domain names for the DNS queries that you want to forward (such as example.com) and the IP addresses of the DNS resolvers on the on-premises network that you want to forward the queries to.
* AWS PrivateLink is a highly available, scalable technology that enables you to privately connect your VPC to supported AWS services, services hosted by other AWS accounts (VPC endpoint services), and supported AWS Marketplace partner services. You can create your own application in your VPC and configure it as an AWS PrivateLink-powered service (referred to as an endpoint service). Other AWS principals can create a connection from their VPC to your endpoint service using an interface VPC endpoint or a Gateway Load Balancer endpoint, depending on the type of service. You are the service provider, and the AWS principals that create connections to your service are service consumers.
* NAT gateways managed by AWS don't accept traffic initiated from the internet. However, if inbound internet traffic is permitted by your security group or Network ACLs then it appears as accepted.
* Only Application Load Balancer (ALB) supports Local Zone.
* You cannot use a Lambda function as a target when using Local Zone subnets for configuring the ELB.
* AWS advertises appropriate Amazon prefixes to you so that you can reach either your VPCs or other AWS services. You can access all AWS prefixes through this connection; for example, Amazon EC2, Amazon S3, and Amazon.com. You do not have access to non-Amazon prefixes. AWS recommends that you use a firewall filter (based on the source/destination address of packets) to control traffic to and from some prefixes. If you're using a prefix filter (route map), ensure that it accepts prefixes with an exact match or longer. Prefixes advertised from AWS Direct Connect may be aggregated and may differ from the prefixes defined in your prefix filter.
* AWS Direct Connect is a networking service that provides an alternative to using the internet to connect to AWS. Using Direct Connect, data that would have previously been transported over the internet is delivered through a private network connection between your facilities and AW.
* AWS Direct Connect (DX) provides three types of virtual interfaces - public, private, and transit.
  * Private virtual interface: A private virtual interface should be used to access an Amazon VPC using private IP addresses.
  * Public virtual interface: A public virtual interface can access all AWS public services using public IP addresses.
  * Transit virtual interface: A transit virtual interface should be used to access one or more Amazon VPC Transit Gateways associated with Direct Connect gateways. You can use transit virtual interfaces with 1/2/5/10 Gbps AWS Direct Connect connections.
* You can combine AWS Direct Connect dedicated network connections with the Amazon VPC VPN. AWS Direct Connect public VIF can be used to establish a dedicated network connection between your network to public AWS resources, such as an Amazon virtual private gateway IPsec endpoint. This solution combines the benefits of the end-to-end secure IPSec connection with low latency and increased bandwidth of the AWS Direct Connect to provide a more consistent network experience than internet-based VPN connections.
* SSL passthrough uses TCP mode to pass encrypted data to servers.
* if you are developing an application that needs to comply with strict external regulations, you might be required to secure all network connections. The following procedure can be used to accomplish this objective:
  * First, add a secure listener to your load balancer
  * You must also configure the instances in your environment to listen on the secure port and terminate HTTPS connections. The configuration varies per platform. You can use a self-signed certificate for the EC2 instances.
  * For end-to-end HTTPS in a load-balanced environment, you can combine instance and load balancer termination to encrypt both connections. By default, if you configure the load balancer to forward traffic using HTTPS, it will trust any certificate presented to it by the backend instances. For maximum security, you can attach policies to the load balancer that prevent it from connecting to instances that don't present a public certificate that it trusts.
  * Lastly, you can configure your database to accept only SSL connections by using the GRANT command with the REQUIRE SSL option.
* To configure the hardware VPN as a backup for your Direct Connect connection:
Be sure that you use the same virtual private gateway for both Direct Connect and the VPN connection to the VPC.
  * If you are configuring a Border Gateway Protocol (BGP) VPN, advertise the same prefix for Direct Connect and the VPN.
  * If you are configuring a static VPN, add the same static prefixes to the VPN connection that you are announcing with the Direct Connect virtual interface.
  * If you are advertising the same routes toward the AWS VPC, the Direct Connect path is always be preferred, regardless of AS path prepending.
  * Be sure that Direct Connect is the preferred route from your end, and not over VPN when the Direct Connect virtual interface is up in order to avoid asymmetric routing; this might cause traffic to be dropped. AWS always prefers a Direct Connect connection over VPN routes.
* To securely serve this private content by using CloudFront, you can do the following:
Require that your users access your private content by using special CloudFront signed URLs or signed cookies.
You should use a signed URL if you want to restrict access to individual files, for example, an installation download for your application. A signed URL includes additional information, for example, expiration date and time, that gives you more control over access to your content.
On the other hand, CloudFront signed cookies allow you to control who can access your content when you don't want to change your current URLs or when you want to provide access to multiple restricted files, for example, all of the files in the members' area of a website.
* A signed URL includes additional information, for example, an expiration date and time, that gives you more control over access to your content. This additional information appears in a policy statement, which is based on either a canned policy or a custom policy.
With the Canned policy, you can specify the date and time that users can no longer access your content. Since each document has a different access expiry date, the policy cannot be reused and has to be created separately for each document. 
* You do not need to contact AWS Support or your AWS Account Manager for the cross-connect details of your Direct Connect connection.
* To configure an Active/Passive connection using a private ASN: Confirm that your customer gateway is advertising the longer prefix on your primary connection.
* Simple AD does not support Microsoft Exchange.
* If you're experiencing idle timeouts due to low traffic on a VPN tunnel:
  * Be sure that there's constant bidirectional traffic between your local network and your VPC. If necessary, create a host that sends ICMP requests to an instance in your VPC every 5 seconds. Review your VPN device's idle timeout settings using information from your device's vendor. When there's no traffic through a VPN tunnel for the duration of your vendor-specific VPN idle time, the IPsec session terminates.
* If your customer gateway device has DPD enabled, be sure that:
  * It's configured to receive and respond to DPD messages.
  * It isn't too busy to respond to DPD messages from AWS peers.
  * It isn't rate-limiting DPD messages due to IPS features enabled in the firewal.
* You cannot have just one Direct Connect connection for multiple on-premises data centers that are in different locations.
* AWS Global Accelerator is a networking service that helps you improve the availability and performance of the applications that you offer to your global users. AWS Global Accelerator is easy to set up, configure, and manage. It provides static IP addresses that provide a fixed entry point to your applications and eliminate the complexity of managing specific IP addresses for different AWS Regions and Availability Zones.
* If you have multiple AWS Site-to-Site VPN connections, you can provide secure communication between sites using the AWS VPN CloudHub. This enables your remote sites to communicate with each other, and not just with the VPC. Sites that use AWS Direct Connect connections to the virtual private gateway can also be part of the AWS VPN CloudHub.
* A gateway endpoint is a gateway that is a target for a route in your route table used for traffic destined to either Amazon S3 or DynamoDB. 
* You can configure CloudFront to add custom headers to the requests that it sends to your origin. These custom headers enable you to send and gather information from your origin that you don’t get with typical viewer requests. These headers can even be customized for each origin. CloudFront supports custom headers for both custom and Amazon S3 origins.
* AWS Direct Connect by itself cannot provide an encrypted connection between a data center and AWS Cloud. 
* With AWS Direct Connect plus VPN, you can combine one or more AWS Direct Connect dedicated network connections with the Amazon VPC VPN. This combination provides an IPsec-encrypted private connection that also reduces network costs, increases bandwidth throughput, and provides a more consistent network experience than internet-based VPN connections. This solution combines the AWS-managed benefits of the VPN solution with low latency, increased bandwidth, more consistent benefits of the AWS Direct Connect solution, and an end-to-end, secure IPsec connection.
* You can configure Amazon Route 53 to log information about the public DNS queries that Route 53 receives, such as the following:
  * Domain or subdomain that was requested
  * Date and time of the request
  * DNS record type (such as A or AAAA)
  * Route 53 edge location that responded to the DNS query
  * DNS response code, such as NoError or ServFail
Once you configure query logging, Route 53 will send logs to CloudWatch Logs. You use CloudWatch Logs tools to access the query logs.
* When you create a LAG, you can download the Letter of Authorization and Connecting Facility Assignment (LOA-CFA) for each new physical connection individually from the AWS Direct Connect console.
* Use Centralized VPC Endpoints for connecting with multiple VPCs, also known as shared services VPC. This is cost-effective.
* When you create a VPC, you must specify an IPv4 CIDR block for the VPC. The allowed block size is between a /16 netmask (65,536 IP addresses) and /28 netmask (16 IP addresses). After you've created your VPC, you can associate secondary CIDR blocks with the VPC. The CIDR block of a subnet can be the same as the CIDR block for the VPC (for a single subnet in the VPC), or a subset of the CIDR block for the VPC (for multiple subnets). The allowed block size is between a /28 netmask and /16 netmask. If you create more than one subnet in a VPC, the CIDR blocks of the subnets cannot overlap.
* Dynamic content, as determined at request time (cache-behavior configured to forward all headers), does not flow through regional edge caches, but goes directly to the origin. So this option is correct. Proxy methods PUT/POST/PATCH/OPTIONS/DELETE go directly to the origin from the POPs and do not proxy through the regional edge caches.
* IP address management (IPAM) is a core part of planning and managing the assignment and use of IP address space of a network. In order to request available CIDR blocks from IPAM for VPCs, you can use AWS CloudFormation Custom Resources.
* A custom routing accelerator is a new type of accelerator in Global Accelerator. It allows you to use your own application logic to deterministically route one or more users to a specific Amazon EC2 instance destination in a single or multiple AWS Regions. This is useful for use cases where you want to control which session on an EC2 instance your user traffic is sent to.
* A Gateway endpoint is a gateway that you specify in your route table to access Amazon S3 from your VPC over the AWS network. Gateway endpoint uses Amazon S3 public IP addresses and does not allow access from on-premises systems.
* You can use two types of VPC endpoints to access Amazon S3: gateway endpoints and interface endpoints. A gateway endpoint is a gateway that you specify in your route table to access Amazon S3 from your VPC over the AWS network. Interface endpoints extend the functionality of gateway endpoints by using private IP addresses to route requests to Amazon S3 from within your VPC, on-premises, or from a VPC in another AWS Region using VPC peering or AWS Transit Gateway. Interface endpoints are compatible with gateway endpoints. If you have an existing gateway endpoint in the VPC, you can use both types of endpoints in the same VPC.
* NAT Gateway is charged on an hourly basis and this charge will contribute to the total cost of NAT Gateway as aside with data processing.
* You can use ALIAS in Route53 to route www.example.com and example.com to an ELB. CNAME records are not suppoter to example.com.
* After you associate a new set of DHCP options with a VPC, any existing instances and all new instances that you launch in the VPC use these options. You don't need to restart or relaunch the instances. They automatically pick up the changes within a few hours, depending on how frequently the instance renews its DHCP lease.
* Steps must be taken to order the cross-connect at the Direct Connect location:
  * Obtain the LOA/CFA from the AWS Management Console when ordering the Direct Connect connection. 
  * Provide it to the APN Partner when ordering connectivity. 
  * The Direct Connect partner will ensure that the cross-connect is installed.
* The public IPv4 address is displayed as a property of the network interface in the console, but it's mapped to the primary private IPv4 address through NAT. Therefore, if you inspect the properties of your network interface on your instance, for example, through ifconfig (Linux) or ipconfig (Windows), the public IPv4 address is not displayed. 
* Configure the ELB protocols in TCP mode. Configure the application instances for SSL termination. Configure Amazon RDS for SSL, and use REQUIRE SSL grants. With that all data will be encrypted.
* Create a outbound rule in a NACL TCP Port Range 1024-65535 to allow HTPP requests.
* Configure CloudFront to use a custom header and configure an AWS WAF rule on the origin’s Application Load Balancer to accept only traffic that contains that header if you want to protect ALB from an attack.
* Use multiple CloudHSM instances to the cluster. Then requests to it will automatically load balance.
* Change the security policy on the ELB to disable vulnerable protocols and ciphers.
* Use AWS CloudFormation custom resource using an AWS Lambda invocatio to use IPAM API to manage IPs. 
* Amazon EC2 instances running in the organization’s VPC must be able to resolve the DNS names of on-premises systems. For that you can deploy and configure a set of EC2 instances into the company VPC to act as DNS proxies. Configure the proxies to forward queries for the on-premises domain to the on-premises DNS systems, and forward all other queries to the Amazon-provided DNS server (172.16.0.2). Change the DHCP options set for the VPC to use the new DNS proxies. Configure the on-premises DNS systems with a stub-zone, delegating the proxies as authoritative for the Route 53 private hosted zone.
* Create a proxy resolver within the VPC. Point the on-premises forwarder to the proxy resolver. With that On-premises users will be able to resolve names in the private hosted zone, although instances in a peered VPC can.
* Your organization has a newly installed 1-Gbps AWS Direct Connect connection. The minimum requirements for your router is 1-Gbps Single Mode Fiber Interface, 802.1Q VLAN, Peer IP Address, BGP Session with MD5.
* EC2 instances must have IPv4 in addition to IPv6, so is the IPv4 range which has to be extended. As a subnet CDIR cannot be modified we need to create a new one, associate the new IPv4 an the existing IPv6, and add it to the group.
* At least two subnets in different Availability Zones. To launch Amazon WorkSpaces and need to configure the appropriate networking resources.
* Configure the CloudFront Cache Behavior to require HTTPS and the CloudFront Origin’s Protocol Policy to 'Match Viewer’ to increase security.
* Use the inter-region capabilities of Direct Connect to establish a private virtual interface from Direct Connect location in one region to the new VPC in another region.
* If you have a Direct connection you can create a new private virtual interface, and leverage the existing connection to connect to the partner VPC to send data from on-premise to this partner VPC.
* Use a Route 53 public and private hosted zone for example.com and perform subdomain delegation for dev.example.com if the name server for subdomain “dev.example.com” should reside on-premises.
* If tou have many private subdomains (sub.example.com) you can create a single Route 53 Private Hosted Zone for the zone sub.example.com and associate it with the three VPCs.
* The Proxy Protocol v2 is an option in NLB which appends the source IP in the TCP packet header if the servers are in on-premise and ALB will not do source IP preservation.
* The NAT gateway does not support fragmented packets.
* BGP advertised routes per route table (propagated routes) is 100. This quota cannot be increased. If you require more than 100 prefixes, advertise a default route.
* If you advertise more than 100 routes over the BGP session, the BGP session will go into an idle state with the BGP session DOWN.
* The maximum S2S VPN per region is 50. 
* Use an Amazon EC2 instance VPN for the desktop, mobile, and partner VPN connections. Use features of the VPN instance to limit routing and connectivity.
* If you configure a proxy on an Amazon EC2 instance launched with an attached IAM role, ensure that you exempt the address used to access the instance metadata. To do this, set the NO_PROXY environment variable to the IP address of the instance metadata service, 169.254.169.254. This address does not vary.
* Once Amazon allocates a network range for your DX, that becomes your range and Amazon will not re-advertise your range to other customers. However all Amazon owned addresses can reach you. 
* To find out available CIDR ranges, a custom logic is required.
* A company has two redundant AWS Direct Connect connections to a VPC. The VPC is configured using BGP metrics so that one Direct Connect connection is used as the primary traffic path. The company wants the primary Direct Connect connection to fail to the secondary in less than one second. For that enable Bidirectional Forwarding Detection (BFD) on the company’s router with a detection minimum interval of 300 ms and a BFD liveness detection multiplier of 3.
* Create a CloudWatch metric that checks the status of the EC2 StatusCheckFailed metric, add an alarm to the metric, and then create a health check that is based on the state of the alarm. This will configure health checks for record sets within the zone that are associated with instances using private hosted zone using Amazon Route 53.
* If traffic failed to switch over to the backup VPN connection confirm that the same routes are being advertised over both the VPN and Direct Connect.
* If the domain name received via DHCP should be different for a particular set of instances that are currently in one particular subnet create a new peered VPC, configure the DHCP option set with the different domain name, and re-launch the required instances there.
* If the origin does not support the ciphers or protocols in the SSL/TLS exchange with CloudFront it can generate HTTP 502 (Bad Gateway).
* When you configure Amazon SQS to send messages from Amazon VPC, you must enable private DNS and specify endpoints in the format sqs.us-east-2.amazonaws.com.
* You have 4 VPCs.You need to set up AWS Direct Connect to enable data flow from on-premises to each VPC with minimun cost. Create a total of four private VIFs, and enable VPC peering between all VPCs.
* If the origin server returns an expired certificate, an invalid certificate, or a self-signed certificate, or if the origin server returns the certificate chain in the wrong order, CloudFront drops the TCP connection, returns HTTP status code 502 (Bad Gateway), and sets the X-Cache header to Error from cloudfront.
* In workspace yo can receive "An error occurred while launching your WorkSpace. Please try again." update the company's corporate firewall to allow outbound access to UDP on port 4172 and TCP on port 4172. Open inbound ephemeral ports explicitly to allow return communication.
* Remember that if questions states that certain URL needs to be whitelisted, then custom proxy server is always needed.
* Whenever you have a second DX connection at same location, AWS will provide a different router.
* You can use host condition to redirect requests to example.com and sub.example.com for example.
* IP protocol50 and UDP port 500 must be released on your Firewall to AWS VPN Connections.
* Your company maintains an Amazon Route 53 private hosted zone. DNS resolution is restricted to a single, pre-existing VPC. For a new application deployment, you create an additional VPC in the same AWS account. To enable DNS resolution both within the new VPC and from the on-premises infrastructure 
  * Launch Amazon EC2-based DNS proxies in the new VPC. Specify the proxies as forwarders in the on-premises DNS 
  * Update the Route 53 private hosted zone’s VPC associations to include the new VPC. 
* An organization will be extending its existing on-premises infrastructure into the cloud. The design consists of a transit VPC that contains stateful firewalls that will be deployed in a highly available configuration across two Availability Zones for automatic failover. You will need BGP and AS prepending.
* You can enable MTU of 9001 on OS to increase network performance of a application.
* Select instance with support for single root I/O virtualization and ensure that propers OS drivers are installed to reduce latency.
* You may need to configure on-premise router to reach AWS.
* 169.254.169.253 is a valid IP in a CIDR range.
* Enable Dead Peer Connection or send ICMP request to VPC each 5 seconds to avoid dead connections.
* If EC2 instances in your VPC are unable to resolve on-premises resources check NACL UDP and TCP 53 port outbound.
* You have two VPCs that require DNS resolution from your on-premises data center and you want to have a DNS server in the cloud, but you don't want to have multiple DNS servers.
  * Peer the VPCs and set up route between them.
  * Configure DHCP route options sets in both VPC to point to the DNS server.
* When configuring Active/Passive HA on VPN tunnels keep both tunnels up and configure MED on one of the tunnels.
* Traffic flow creator can reduce latency.
* Hosted AD can minimize traffic.
* Virtual Private Gateway and Customer Gateway are always required for VPN.
* Use MED or AS_PATH prepeding to influence the direction of Dynamic VPN traffic over multiple link.
* To run VPN over DX, you need to have a public VIF to access the VPN endpoints. This will be encrypted.
* When the user data is more random and not generated at regular intervals, there can be a period which has no associated data. The user can either publish the zero (0) value for that period or not publish the data at all. It is recommended that the user should publish zero instead of no value to monitor the health of the application.
* Instances cannot change subnets, so a new instance must be created.
* Simple AD is not a full Active Directory server and will not work with many MS products.
* You cannot send a broadcast in an AWS VPC, but the address is still reserved.
* You have a hybrid infrastructure, and you need AWS resources to be able to resolve your on-premises DNS names. You have configured a DNS server on an EC2 instance. For that you need to configure the DHCP option set in the VPC to point to the EC2 DNS server.
* The Intel interface has a max speed of 10 Gbps and the ENA is upto 100 Gbps. The speed will be the lesser of the two.
* If your network utilizes jumbo frames on its servers and your router. You are trying to access your AWS resources, and you are having issues with packet loss. To solve that you can remove the "Do not Fragment" flag on the packets.
* In the APi create a Reusable Delegation Set if you have a domain using another registrar and wants to use the same nameservers as your current domain hosted with AWS.
* A Customer Gateway would allow you to add a new datacenter to your VPN.
* Your company has two DX locations. You need to configure one link as passive. For that you can configure AS_PATH Prepending on the link 
* Sub-1G service is only available through AWS partners.
* The DDoS isn't a TCP attack.
* You can only have 1 instance of any VLAN ID.
* You need your data center to be able to resolve Route 53 queries in your private hosted zone. If your VPC has a CIDR 10.1.0.0/16 configure your DNS server to forward queries for the private hosted zone to 10.1.0.2.
* To acquire best transmission rates inside AWS, Jumbo frame should be used, so MTU is better to be set at 9001. For traffic towards the internet, the AWS, MTU 1500 should be selected for best compatibility.
* The DX Gateway will allow access to multiple regions.
* The Differentiated Services Code Point value, or DSCP, is used to label packets on QoS enabled networks for prioritization.
* /56 is the IPv6 subnet CIDR used by a VPC.
* When configuring redundant connections with the AWS Direct Connect, and to provide for failover, we recommend that you request and configure two dedicated connections to the AWS. There are different configuration choices available when you provision two dedicated connections. You can either use Active/  Active (BGP multipath) connection or Active/Passive (failover) connection to configure the two dedicated connections.
* BGP MED is used to steer traffic and not for requesting a VIF.
* The path selection process always chooses the most specific prefix first.
* All links must be the same speed for a LAG to be operational.
* You must complete a LOA for each new physical connection.
* Amazon VPC does not support multicast nor broadcast.
* Any data transfer out of a remote region is billed at the remote region data transfer rate.
* The higher CIDR or more specific route will always take precedence.
* o use the AWS Direct Connect, after you have created a virtual interface for your AWS Direct Connect connection, you can download the router configuration file. This configuration helps your router connect to AWS Direct Connect router. This configuration is related to your created virtual interface details and vendor, platform, and software of your router.
* You get 2 tunnels with each VPN connection hosted by AWS.
* Allow ISAKMP (UDP port 500) and Encapsulating Security Payload (IP protocol 50) traffic to route between your network and VPN endpoints. If you're using Network Address Translation Traversal (NAT-T), also be sure to allow UDP port 4500.
* An ELB Classic Load Balancer cannot validate a client side certificate, so it must be passed through as standard TCP on port 443 to let the EC2 instance handle the validation.
* By default, a VPN has two tunnels for high availability.
* The clear requirements for setting up LAG are given in the AWS Documentation. The following rules apply:
  * All connections in the LAG must use the same bandwidth. The following bandwidths are supported: 1 Gbps and 10 Gbps.
  * You can have a maximum of 4 connections in a LAG. Each connection in the LAG counts towards your overall connection limit for the region.
  * All connections in the LAG must terminate at the same AWS Direct Connect endpoint.
* AWS recommends enabling BFD when configuring multiple AWS Direct Connect connections or when configuring a single AWS Direct Connect connection and a VPN connection as a backup to ensure fast detection and failover.
* Change the MTU setting on the network interface for each instance if you want to ensure that a minimal number of packets can be sent across the network interfaces.
* Jumbo frames allow more than 1500 bytes of data by increasing the payload size per packet, thus increasing the packet's percentage that is not packet overhead. Fewer packets are needed to send the same amount of usable data.
* Since transitive peering is not allowed, you can use a proxy instance to forward the requests.
* DPDK is the Data Plane Development Kit that consists of libraries to accelerate packet processing workloads running on a wide variety of CPU architectures.
* If you get an InsufficientInstanceCapacity error when you try to launch an instance or restart a stopped instance, AWS does not currently have enough available On-Demand capacity to service your request.
* You can’t configure two different IAM permissions for a single hosted zone. You must provide two separate hosted zones in order to attach a unique IAM Permission for each zone.
* Configure the Elastic Beanstalk environment’s EC2 instances to terminate the SSL/TLS connection for RDS. Modify the load balancer to use TCP and set the RDS to accept only SSL connections by using the GRANT command with the REQUIRE SSL option.
* Set up an Alias A Record for tutorialsdojo.com with the ALB as the target. For the www.tutorialsdojo.com subdomain, create a CNAME record that points to the ALB.
* To create a public virtual interface, you must supply the following:
  * For Virtual interface name, enter a name for the virtual interface.
  * For Connection, choose the Direct Connect connection that you want to use for the interface.
  * For VLAN, enter the ID number for your virtual local area network (VLAN).
  * For BGP ASN, enter the Border Gateway Protocol Autonomous System Number of your on-premises peer router for the new virtual interface. The valid values are 1-2147483647.
  * For the ‘Prefixes you want to advertise’ field, enter the IPv4 CIDR destination addresses (separated by commas) to which traffic should be routed over the virtual interface.
* For HTTP Only, CloudFront solely uses HTTP to access the origin. For HTTPS Only, CloudFront uses only HTTPS to access the origin and for Match Viewer, CloudFront communicates with your origin using HTTP or HTTPS, depending on the protocol of the viewer request. CloudFront caches the object only once even if viewers make requests using both HTTP and HTTPS protocols.
* When you use AWS Direct Connect to transport production workloads to and from AWS services, it’s a best practice to create two DX connections through different data centers or providers. You have two options on how to configure your connections:
  * Active/Active – Traffic is load-shared between interfaces based on flow. If one connection becomes unavailable, all traffic is routed through the other connection.
  * Active/Passive – One connection handles traffic, and the other is on standby. If the active connection becomes unavailable, all traffic is routed through the passive connection.
* After you create a set of DHCP options, you can’t modify them. If you want your VPC to use a different set of DHCP options, you must create a new set and associate them with your VPC. You can also set up your VPC to use no DHCP options at all. After you associate a new set of DHCP options with the VPC, any existing instances and all new instances that you launch in that VPC use the new options. You don’t need to restart or relaunch the instances. They automatically pick up the changes within a few hours, depending on how frequently the instance renews its DHCP lease. If you want, you can explicitly renew the lease using the operating system on the instance.
* To use your AWS Direct Connect connection with another AWS account, you can create a hosted virtual interface for that account. The owner of the other account must accept the hosted virtual interface to begin using it. A hosted virtual interface works the same as a standard virtual interface and can connect to public resources or a VPC. You can create a hosted virtual interface for accounts within your AWS Organizations, or AWS Organizations that are different from yours. You must accept the virtual interface before you can use it.
* AWS CloudHSM provides hardware security modules (HSMs) in a cluster. A cluster is a collection of individual HSMs that AWS CloudHSM keeps in sync. You can think of a cluster as one logical HSM. When you perform a task or operation on one HSM in a cluster, the other HSMs in that cluster are automatically kept up to date. When you create the HSMs in different AWS Availability Zones, you automatically get high availability.
* Limiting outbound traffic to certain trusted domains (called “whitelisting”) you help prevent instances from downloading malware, communicating with bot networks, or attacking internet hosts. You can use Squid, a leading open-source proxy, to implement a transparent proxy that can restrict both HTTP and HTTPS outbound traffic to a given set of Internet domains, while being fully transparent for instances in the private subnet.
* The following are the things you have to consider when establishing an Active/Passive connection:
If you’re using a public ASN:
  * Confirm that your customer gateway is advertising the same prefix (public IP or network that you own) on both Border Gateway Protocol (BGP) sessions.
  * You can use the BGP AS_Path attribute such that the prefixes advertised from the secondary connection are prepended with the customer gateway ASN twice. For example, if your customer gateway uses ASN 123, it can advertise the prefix on the secondary connection with AS_Path set to 123 123.
  * You can use the BGP Local Preference attribute such that the customer gateway accepts routes from the primary connection as 200 and the secondary connection as 100. A higher Local Preference value is preferred, and the default is 100.
  * The primary connection is considered the primary path. In the event of a failure, traffic is shifted to the secondary connection as a secondary path.
If you’re using a private ASN:
  * Confirm that your customer gateway is advertising the longer prefix on your primary connection. For example, if you’re advertising prefix X.X.X.0/24, then your customer gateway can advertise two prefixes (X.X.X.0/25 and X.X.X.128/25) on your primary connection and prefix X.X.X.0/24 on your secondary connection.
  * If both interfaces are in the UP state, and the longer prefix is advertised on your primary connection, then traffic is sent to your customer gateway through the primary connection. In the event of a failure, traffic is shifted and sent to the secondary connection.
* If you use custom DNS domain names defined in a private hosted zone in Amazon Route 53, the enableDnsHostnames and enableDnsSupport attributes must be set to true.
* If you are only using a single AWS Direct Connect location, you have to create another Direct Connect connection to another AWS Direct Connect location to improve the connection resiliency.
* Equal-cost multi-path routing (ECMP) is available with AWS Site-to-Site VPN on AWS Transit Gateway to help increase the traffic bandwidth over multiple paths. You can use ECMP to get higher VPN bandwidth, than the default VPN bandwidth limit of 1.25 Gbps,  by aggregating multiple VPN connections.
* Network Load Balancers use Proxy Protocol version 2 to send additional connection information such as the source and destination.
* If the physical connection is down, or there is no connectivity between the BGP peers. You have to check and verify the configuration on your Direct Connect router by doing the following steps:
  * The IP addresses of the local and remote BGP peers, local and remote BGP Autonomous System Numbers (ASN), and the BGP MD5 password must be configured with the downloaded Direct Connect configuration file from the AWS Direct Connect console.
  * Verify that the Direct Connect router or any other device is not blocking ingress or egress from TCP port 179 and other appropriate ephemeral ports.
  * BGP peers can’t be more than one hop away from each other, because external BGP (EBGP) Multi-hop is disabled on the AWS end.
* Amazon RDS supports using Transparent Data Encryption (TDE) to encrypt stored data on your DB instances running Microsoft SQL Server. 
* When a virtual private gateway receives routing information, it uses path selection to determine how to route traffic. Longest prefix match is also used for the path selection. If the prefixes are the same, then the virtual private gateway prioritizes routes as follows, from MOST preferred to LEAST preferred:
  * BGP propagated routes from an AWS Direct Connect connection
  * Manually added static routes for a Site-to-Site VPN connection
  * BGP propagated routes from a Site-to-Site VPN connection
  * For matching prefixes where each Site-to-Site VPN connection uses BGP, the AS PATH is compared and the prefix with the shortest AS PATH is preferred. Alternatively, you can prepend AS_PATH, so that the path is less preferred.
  * When the AS PATHs are the same length and if the first AS in the AS_SEQUENCE is the same across multiple paths, multi-exit discriminators (MEDs) are compared. The path with the lowest MED value is preferred.
* If your AWS Direct Connect physical connection is up but your virtual interface is down, use the following steps to troubleshoot the issue.
  * If you cannot ping the Amazon peer IP address, verify that your peer IP address is configured correctly and in the correct VLAN. Ensure that the IP address is configured in the VLAN subinterface and not the physical interface (for example, GigabitEthernet0/0.123 instead of GigabitEthernet0/0).
  * Verify if the router has a MAC address entry from the AWS endpoint in your address resolution protocol (ARP) table.
  * Ensure that any intermediate devices between endpoints have VLAN trunking enabled for your 802.1Q VLAN tag. ARP cannot be established on the AWS side until AWS receives tagged traffic.
 * Clear your or your provider’s ARP table cache.
* A link aggregation group (LAG) is a logical interface that uses the Link Aggregation Control Protocol (LACP) to aggregate multiple connections at a single AWS Direct Connect endpoint, allowing you to treat them as a single, managed connection. You can create a LAG from existing connections, or you can provision new connections. After you’ve created the LAG, you can associate existing connections (whether standalone or part of another LAG) with the LAG.
* You can protect your domain from DNS spoofing or a man-in-the-middle attack, by configuring Domain Name System Security Extensions (DNSSEC), a protocol for securing DNS traffic.
* With a public virtual interface, you can:
  * Connect to all AWS public IP addresses globally.
  * Create public virtual interfaces in any DX location to receive Amazon’s global IP routes.
  * Access publicly routable Amazon services in any AWS Region (except the AWS China Region).
* The following are some of the tunnel options that you can configure for your VPN connection:
  * Dead peer detection (DPD) timeout – The duration after which DPD timeout occurs. You can specify 30 or higher
  * IKE versions – The IKE versions that are permitted for the VPN tunnel. You can specify one or more of the default values.
  * Inside tunnel CIDR – The range of inside IP addresses for the VPN tunnel. You can specify a size /30 CIDR block from the 169.254.0.0/16 range. The CIDR block must be unique across all Site-to-Site VPN connections that use the same virtual private gateway.
  * Phase 1 Diffie-Hellman (DH) group numbers – The DH group numbers that are permitted for the VPN tunnel for phase 1 of the IKE negotiations. You can specify one or more of the default values.
  * Pre-shared key (PSK) – The pre-shared key (PSK) to establish the initial internet key exchange (IKE) security association between the virtual private gateway and customer gateway.
  * Phase 2 Diffie-Hellman (DH) group numbers – The DH group numbers that are permitted for the VPN tunnel for phase 2 of the IKE negotiations. You can specify one or more of the default values.
* You can use a web server variable (e.g. REMOTE_ADDR) to get the IP addresses of the users who are visiting your website
* If your web server is connected to the Internet through a load balancer, a web server variable might contain the IP address of the load balancer, not the IP address of the user.
* The last IP address in the X-Forwarded-For HTTP header is most likely associated with the user’s geographic location. This header typically contains more than one IP address, most of which are for proxies or load balancers.
* When associating a VPC from an external AWS account, you have to be mindful of the following:
  * If you want to associate multiple VPCs that you created with one account with a hosted zone that you created with a different account, you must submit one authorization request for each VPC.
  * When you authorize the association, you must specify the hosted zone ID, so the private hosted zone must already exist.
  * You can’t use the Route 53 console either to authorize the association of a VPC with a private hosted zone or to make the association.
* The communities 7224:1 – 7224:65535 are reserved by AWS Direct Connect. AWS Direct Connect applies the following BGP communities to its advertised routes:
  * 7224:8100—Routes that originate from the same AWS Region in which the AWS Direct Connect point of presence is associated.
  * 7224:8200—Routes that originate from the same continent with which the AWS Direct Connect point of presence is associated.
  * No tag—Global (all public AWS Regions).
* The intrinsic function ***Fn::Cidr*** returns an array of CIDR address blocks. The number of CIDR blocks returned is dependent on the count parameter. This function has three parameters:
  * ***ipBlock*** – The user-specified CIDR address block to be split into smaller CIDR blocks.
  * ***count*** – The number of CIDRs to generate. Valid range is between 1 and 256.
  * ***cidrBits*** – The number of subnet bits for the CIDR. For example, specifying a value “8” for this parameter will create a CIDR with a mask of “/24”.
* To connect to your resources hosted in an Amazon VPC (using their private IP addresses) through a transit gateway, use a transit virtual interface. With a transit virtual interface, you can:
  * Connect multiple VPCs in the same or different AWS account using DX.
  * Associate up to three transit gateways in the same AWS Region when you use a transit virtual interface to connect to a DX gateway.
  * Attach VPCs in the same AWS Region to the transit gateway. Then, access multiple VPCs in different AWS accounts in the same AWS Region using a transit virtual interface.
* AWS Global Accelerator is a service that improves the availability and performance of your applications with local or global users. It provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your Application Load Balancers, Network Load Balancers, or Amazon EC2 instances.
* A prefix list is a set of one or more CIDR blocks. There are two types of prefix lists:
  * ***AWS-managed prefix-list*** — Represents the IP address ranges for an AWS service. You can reference an AWS-managed prefix-list in your VPC security group rules and in subnet route table entries. For example, you can reference an AWS-managed prefix-list in an outbound VPC security group rule when connecting to an AWS service through a gateway VPC endpoint. You cannot create, modify, share, or delete an AWS-managed prefix list.
  * ***Customer-managed prefix-list*** — A set of IPv4 or IPv6 CIDR blocks that you define and manage. You can reference the prefix-list in your VPC security group rules and in subnet route table entries. This enables you to manage the IP addresses that you frequently use for these resources in a single group, instead of repeatedly referencing the same IP addresses in each resource. You can share your prefix list with other AWS accounts, enabling those accounts to reference the prefix-list in their own resources.
* You can bring part or all of your public IPv4 address range from your on-premises network to your AWS account. You continue to own the address range, but AWS advertises it on the Internet. After you bring the address range to AWS, it appears in your account as an address pool. You can create an Elastic IP address from your address pool and use it with your AWS resources, such as EC2 instances, NAT gateways, and Network Load Balancers. This is also called “Bring Your Own IP Addresses (BYOIP)”.
To ensure that only you can bring your address range to your AWS account, you must authorize Amazon to advertise the address range and provide proof that you own the address range. A Route Origin Authorization (ROA) is a document that you can create through your Regional internet registry (RIR), such as the American Registry for Internet Numbers (ARIN) or Réseaux IP Européens Network Coordination Centre (RIPE). It contains the address range, the ASNs that are allowed to advertise the address range, and the expiration date.
* The following local preference BGP community tags are supported:
  * 7224:7100 — Low preference
  * 7224:7200 — Medium preference
  * 7224:7300 — High preference
* The public address of an EC2 instance can't be fetched by using the ifconfig (Linux) or ipconfig (Windows) commands. You have to call the instance metadata service instead. 
* An Elastic Fabric Adapter (EFA) is a network device that you can attach to your Amazon EC2 instance to accelerate High-Performance Computing (HPC) and machine learning applications. EFA enables you to achieve the application performance of an on-premises HPC cluster, with the scalability, flexibility, and elasticity provided by the AWS Cloud.
* 169.254.169.123 is and IP address to use to properly configure the NTP settings.
* You can disassociate a CIDR block that you’ve associated with your VPC; however, you cannot disassociate the CIDR block with which you originally created the VPC (the primary CIDR block).
* RFC 1918 CIDR blocks are basically private IPv4 address ranges as shown as follows:
  * 10.0.0.0       – 10.255.255.255 (10/8 prefix)
  * 172.16.0.0    – 172.31.255.255 (172.16/12 prefix)
  * 192.168.0.0  – 192.168.255.255 (192.168/16 prefix)
If your primary CIDR block is publicly routable (non-RFC 1918), or if it is a CIDR block from the 100.64.0.0/10 range then you can only add publicly routable IPv4 CIDR blocks or a CIDR block from the 100.64.0.0/10 range. 
* AWS Cloud Map extends the capabilities of the Route 53 Auto Naming APIs by providing a service registry for resources, such as IPs, URLs, and ARNs, and offering an API-based service discovery mechanism with a faster change propagation and the ability to use attributes to narrow down the set of discovered resources. Existing Route 53 Auto Naming resources are upgraded automatically to AWS Cloud Map.