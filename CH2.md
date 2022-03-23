# Azure 900 - Chapter 2 - Services

## Azure Virtual Machine

![Azure Virtual Machine](./icon/vm.svg)

### Key characteristics

- IaaS service
- Total control over the OS and the software
- Supports custom OS images
- Well suited for applications that require custom system configuration
- Lift-and-shit scenarios

### Pricing

- You pay for the VM as long as it is running
- You can stop the VM to stop the billing. ***Attention***
  - You can't use the VM while stopped
  - If you don't have a static IP address configured, your IP will likely change when the VM is started

### Downtime

VMs are susceptible to downtime due to three types of events: *planned maintenance*, *unplanned maintenance*, and *unexpected downtime*.

#### Planned maintenance

- Planned updates that Microsoft makes to the host computer
- OS updates
- Driver updates

#### Unplanned maintenance

- Monitoring services detect that your VM's host computer might fail soon
- That computer will be flagged for unplanned maintenance
- Azure will attempt to move your VM to a healthy host computer
- The move takes a short time, and the VM is in a paused state. If the operation fails, the VM will experience *unexpected downtime*

### Availability sets

![Azure VM availability sets](./icon/vm-availability-sets.svg)

*Availability sets* protect you from maintenance events and downtime caused by hardware failure. Azure does that by creating some underlying entities in an availability set called *update domains* and *fault domains*.

#### Fault domains

- Logical representation of the physical rack in which a host computer is installed
- By default, Azure assigns 2 fault domains to an ***availability set***
- If a problem occurs in one fault domain, the VMs in the other fault domain won't be affected
- Protects against: ***unplanned maintenance*** and ***unexpected downtime***

#### Update domains

- By default, Azure assigns 5 update domains to an ***availability set***. These are spread access the ***fault domains*** in the ***availability set***
- Azure reboots VMs in one update domain at a time, waiting 30 minutes for computers to recover before moving to the next update domain
- Protect against: ***planned maintenance***

#### Disadvantages

- Every VM in a ***availability set*** has to be explicitly created
- In cases in which your VM serves a web application, you will need to configure a *load balancer* to handle the the traffic and routing
- Redundancy costs more
- Not compatible with ***availability zones**

### Scale sets

![Azure VM scale sets](./icon/vm-scale-sets.svg)

- *Scale sets* are deployed in ***availability sets***
- You automatically benefit from ***fault domains*** and ***update domains**
- Compatible with ***availability zones***, so you are protected from problems in an Azure *datacenter*
- You can configure scaling rules based on metrics such as CPU, disk usage, network usage, and so forth
- Based on the **auto-scale providers**, *scale sets* allow you to automatically add or remove VMs based on the metrics mentioned above
- It helps reducing costs

### SLA

- Single-instance VM with premium storage: 99.9%
- Multi-VM deployment: 99.95%

## Virtual Network (VNet)

![Azure VNet](./icon/vnet.svg)

*Azure Virtual Network (VNet)* enables Azure resources (e.g., VMs) to securely communicate with each other, the internet, and on-premises networks.

### Key characteristics

- Enables secure communication between Azure resources, the Internet, and on-premises networks
- Allows network traffic filtering and routing
- You can break the VNet in multiple subnets and distribute the IP address space
- You can configure rules to control the connectivity between subnets

### Pricing

Free of cost.

### Public IP Address

![Public IP Address](./icon/public-ip-address.svg)

*Azure Public IP address* enables inbound communication from the Internet to an Azure resource (e.g., a VM), and outbound connectivity to the Internet using a predictable IP address.

### Network security group

![Network Security Group](./icon/network-security-group.svg)

*Azure Network Security Groups* enables network traffic filtering by allowing the creation of multiple inbound and outbound security rules.

### VNet peering

Allows communication between Azure VNets. This enables resources in either VNet to communicate with each other.

#### Key characteristics

- VNet peering is of two types:
  - VNet peering: Connects VNets within the same Azure region
  - Global VNet peering: Connects VNets across Azure regions
- The traffic is not encrypted, however, it travels over Azure's private backbone infrastructure, and not over the Internet

## Azure VPN Gateway

![Azure VPN Gateway](./icon/vpn-gateway.svg)

### Key characteristics

- Azure VPN Gateway uses VPN connections to enable secure connectivity
- Allows encrypted communication between Azure VNets and on-premises networks over the *public Internet*
- Can also be used between Azure VNets as well, and the traffic goes the Microsoft network
- It uses Internet protocol security (IPSec) and the Internet key exchange (IKE) protocols

### Pricing

You pay for two things: the hourly compute costs for the virtual network gateway, and the egress data transfer from the virtual network gateway.

### Gateway types

#### VPN

Creating a *VPN* gateway resource can take up to 45 minute before it is ready for use. There are three connection types supported by a VPN gateway: *VNet-to-VNet*, *site-to-site*, and *point-to-site*.

##### VNet-to-VNet

The VNets you connect can be:

- in the same or different regions
- in the same or different subscriptions
- in the same or different deployment model (i.e., classic vs Resource Manager)

<img src="https://docs.microsoft.com/en-us/azure/vpn-gateway/media/design/vpngateway-vnet-to-vnet-connection-diagram.png" alt="VNet-to-VNet connection">

##### Site-to-site

This type of gateway connection enables a connection from a VNet to an on-premises network using encrypted VPN connection. It also requires a device located on-premises that has a public IP address assigned to it.

<img src="https://docs.microsoft.com/en-us/azure/vpn-gateway/media/design/vpngateway-site-to-site-connection-diagram.png" alt="Site-to-site connection">

##### Point-to-site

A Point-to-Site (P2S) VPN gateway connection lets you create a secure connection to your VNet from an individual client device. This device can be a computer, a mobile device, a tablet or a smartphone.

<img src="https://docs.microsoft.com/en-us/azure/vpn-gateway/media/design/point-to-site.png" alt="Point-to-site connection">

#### ExpressRoute

![Azure ExpressRoute](./icon/vpn-gateway-express-route.svg)

##### Key characteristics

- Can offer up to 10 Gbps network speed over dedicated fiber-optic connections
- Connections are made from your on-premises network to a Microsoft Enterprise Edge (MSEE) router, which then, connects you to Azure
- The MSEE router sits on the edge of Microsoft's network
- The ExpressRoute data does not traverse the public Internet, thus bandwidth is much more reliable

##### Advantages over the VPN type

The VPN gateway type has some limitations, such as a maximum of 1.25 Gbps in network speed. Moreover, the traffic is sent over the public Internet.

