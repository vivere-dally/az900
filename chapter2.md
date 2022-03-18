# Chapter 2

## Web App (App Service)

<img src="https://azurecomcdn.azureedge.net/cvt-7a361c6a8f008ba8dfda7046bb3daedab876505f28e919b6f79a76a47b236a7c/svg/app-service.svg" alt="App Service Img" width="50"/>

Web apps allow you to run applications by providing a preconfigured VM with a runtime stack (Java, .NET, PHP, etc.), or inside a Docker container.

Web apps are running on an App Service Plan VM, which can host multiple web apps.

![Create an App Service](./img/createAppService.png)

Azure Web Apps are PaaS services and they provide a lot of configurations.

## Azure Container Instances (ACI)

<img src="https://docs.microsoft.com/en-us/answers/topics/25412/icon.html?t=282211" alt="ACI" width="50">

Azure Container Instances (ACI) is a PaaS service which allows you to run containerized applications easily.

![Create an ACI](./img/createACI.png)

To run an application by using ACI, you have to specify the following settings:

- where the Docker image is located
- CPU and Memory
- a DNS label and configure the Ports mapping

**Tip** Changing the docker image or the DNS label is not possible after creation.

## Azure Kubernetes Service (AKS)

<img src="https://img.stackshare.io/service/9133/Azure-Container-Service_COLOR-300x300.png" alt="AKS" width="50">

AKS is a container orchestration service, meaning that it is responsible for monitoring and ensuring that containers are always running. It also can scale up or down the number of containers based on the workload needed to be accommodated. Kubernetes has the following properties:

- it creates containers in a pod
- a pod represents a group of related containers which can share resources
- containers in one pod cannot share resources with containers from another pod
- the computer that runs a pod is called a *worker* or a *node*
- a node has a container runtime such as Docker installed alongside Kubernetes services
- the nodes are managed by a *master* node
- the entire environment is called a Kubernetes cluster

## Virtual Network (VNet)

<img src="https://symbols.getvecta.com/stencil_28/71_virtual-network.8cd684329b.png" alt="VNet" width="50">

VNet allows Azure services to communicate with each other and with the Internet. It also allows communication between Azure resources and on-premise resources. A VNet address space can be divided into multiple subnets. You can configure rules that control connectivity between subnets.

When creating a VM, you could use a VNet created beforehand or you can let Azure create a new VNet for you. Without a VNet you could not use a VM.

The IP address that the VNet creates are all private IP addresses. If you want to use VM as a IaaS service for an application, you would also need to create a Public IP Address resource and assign that to the VNet.

<img src="https://azure.microsoft.com/svghandler/ip-addresses/?width=600&height=315" alt="Public IP Address" width="50">

VNet also allow for a Network Security Group to be assigned. That resource enforces rules about what kind of traffic is allowed to the VNet.

<img src="https://wedoazure.files.wordpress.com/2019/08/image-27.png" alt="Network Security Group" width="80">

## Azure VPN Gateway

<img src="https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/images/vpn.png" alt="VPN Gateway" width="1000">

A VPN Gateway is used in cases where two or more VNets need to communicate, or if you want a VNet to communicate with on-premise resources. The traffic will travel over the internet, so to add a layer o security for the network traffic, you can use a virtual private network (VPN) connection.

Azure VPN Gateway uses VPN connections to enable secure connectivity between Azure VNets and other networks. It uses Internet protocol security (IPSec) and the Internet key exchange (IKE) protocols.

The VPN Gateway is running on top of two or more VMs that are created inside a subnet. They are created explicitly for the VPN Gateway and you cannot remote into them or change their configurations.

### Gateway type - VPN

Creating a VPN gateway resource can take up to 45 minute before it is ready for use. There are three connection types supported by a VPN gateway: VNet-to-VNet, site-to-site, and point-to-site.

#### VNet-to-VNet

Each VNet needs to have a VPN Gateway configured. The VNets do not have to be in the same region, or even in the same Azure subscription. Communication between VNets is done using the Azure backbone infrastructure, not over the internet.

VPN Gateways come with pricing tiers, thus based on your tier you could experience bandwidth restrictions. VNet peering comes with no such bandwidth restrictions.

#### Site-to-site

Enables connection from a VNet to an on-premises network using encrypted VPN connection. You must configure a VPN device on your on-premises network, which must have a public-facing IP address. The network traffic will travel over encrypted VPN connection.

These types of connections can authenticate by using Azure certificate authentication, Remote Authentication Dial-In User Service (RADIUS) authentication, Azure Active Directory, or OpenVPN.

#### Point-to-site

This type of connection allows you to connect your VNet to a single device. This device can be a computer, a mobile device, a tablet or a smartphone.

### Gateway type - ExpressRoute

The VPN gateway type has some limitations, such as a maximum of 1.25 Gbps in network speed. Moreover, the traffic is sent over the public Internet.

The ExpressRoute type can offer up to 10 Gbps over dedicated fiber-optic connections. The connection is made from your on-premises network to a Microsoft Enterprise Edge router (MSEE), and the MSEE router then connects you to Azure. The MSEE router sits on the edge of Microsoft's network, and in most cases, your connection will also be from a router in your on-premises network that is on the edge of your network.

Because data in ExpressRoute doesn't traverse the public Internet, bandwidth is much more reliable. However, the ExpressRoute configuration requires that you trust your service provider because the data flows through the circuit. There is an offering called ExpressRoute Direct which provides much higher bandwidth, and where the service provider is removed from the picture.

### Virtual network peering

Allows you to connect VNets. The traffic travels over Azure's private backbone infrastructure, and not over the Internet. However, the traffic is not encrypted. VNet peering allows you to connect VNets in the same region, or in different regions (global virtual network peering). There is one limitation with global peering: if there are resources behind a Azure Load Balancer running in the Basic Tier, you won't be able to connect to those resources using the public IP address of the load balancer. If that's a requirement, you need to upgrade the load balancer to a Standard tier.

## Azure Storage Account

<img src="https://ms-azuretools.gallerycdn.vsassets.io/extensions/ms-azuretools/vscode-azurestorage/0.13.0/1643236289029/Microsoft.VisualStudio.Services.Icons.Default" alt="Storage Account" width="50">

### Blob storage

Binary Large Objects (Blob) referrers to data such as text files, images, videos, documents and many more. Azure Blob Storage is designed for storing unstructured data. An entity stored in Blob Storage is referred to as a blob. There are a couple types of blobs:

- **Block blob**: used to store files used by an application
- **Append blobs**: used to store files that are often updated, such as diagnostic logs
- **Page blobs**: used to store hard disk (.vhd) files

Blobs are organized in containers.

Uploading data from on-premises to Azure Blob Storage can be done via tools such as Azure Storage Explorer or Data Box for large amounts of data.

### Files storage

Azure Files storage is a managed file share that can be mounted, such as Server Message Block (SMB) file shares. Azure File shares can be mounted to Azure VMs and on-premises Windows, Linux, and MacOS. Because they use SMB, you will need the TCP port 445 to be open on your network.

### Storage Account tiers

#### Hot Access

This type of access is recommended for data that is accessed often. It has the highest cost of storage, but the lowest cost of access.

#### Cool Access

This type of access is recommended for data that is not accessed often but intended to be kept for a longer period. It has a low cost of storage, but the access cost is higher.

#### Archive

This type of access is recommended for long-term data storage. If you delete data sooner than 180 days that it got uploaded, you will be charged with a deletion fee. This type of data is not designed for quick and frequent access. The price of storage is the lowest, but the price of access is the highest. The Hot and Cool tiers guarantee access to the first byte of data within milliseconds, whereas with the archive tier that guarantee is within 15 hours.

## Azure Disk Storage

<img src="https://azure.microsoft.com/svghandler/managed-disks/?width=600&height=315" alt="Disk Storage" width="50">

Azure Disk Storage is used by Azure VMs, by storing the VM OS data and application data.

Azure disks are available as both HDDs and SSDs. HDDs are cheaper and designed for noncritical data, whereas SSD are designed for light use (Standard tier) and heavy use (Premium tier).

There are two types of disk storage:

- unmanaged

You can use Azure Storage account to store the .vhd files in page blobs. This is troublesome as you need to manage the Azure Storage Account resource.

- managed

Azure creates a separate resource and handles everything behind the scenes: the storage account, and storage limitations. All you need to worry about is your disk, Azure manages everything else.

## Azure Cosmos DB

<img src="https://gotcosmos.com/images/about/cosmos-logo.svg?v=TV8GAN6U90A78jwat9z4a3cLY6dIphJm8XyfL_NkOjw" alt="Azure Cosmos DB" width="50">

Azure Cosmos DB is a multi-model globally distributed database service.

|      System      |      Description                                                                                                                                                                                                                       |      Common    Use                                                                                                                                                                                                                                                 |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     Key-value    |     Stores data that is tied to a   unique key. Pass in the key and the database returns the data.                                                                                                                                     |     Because the value can be just   about anything, key-value databases have many uses.                                                                                                                                                                            |
|     Column       |     NoSQL databases are called keyspaces,   and a keyspace contains column families. A column contains rows and columns   like a relational table, but each row can have its own set of columns. You   aren’t locked into a schema.    |     Storing user-profile data for a   website. Also, because column databases scale well and are extremely fast,   they are well-suited to storing large amounts of data.                                                                                          |
|     Document     |     Data is stored as a structured   string of text called a document. This can be HTML, JSON, and so forth. This   is similar to a key-value database, except that the document is a structured   value.                              |     Same as key-value, but document   databases have advantages. They scale well horizontally, and they allow you   to query against the value and return portions of the value. A key-value   database query returns the entire value associated with the key.    |
|     Graph        |     Stores data and the relationships   between each piece of data. Data is stored in nodes, and relationships are   drawn between nodes.                                                                                              |     Many systems use graph databases   because they are extremely fast. A social network might use a graph database   because it would be easy to store relationships between people, things those   people like, and so forth.                                    |

When you create a Cosmos DB database, you choose the API you want to use, which determines the database type for your database. The database API types are:

- **Core (SQL)** Creates a document database that you can query using SQL syntax that you might be familiar with from using relational databases.
- **Azure Cosmos DB for MongoDB API** Used for migrating a MongoDB database to Cosmos DB. MongoDB databases are document databases.
- **Cassandra** Used for migrating a Cassandra database to Cosmos DB. Cassandra databases are column databases.
- **Azure Table** Used for migrating data stored in Azure Table Storage to Cosmos DB. This creates a key-value database.
- **Gremlin** Used for migrating Gremlin databases to Cosmos DB. Gremlin databases are graph databases.

Microsoft calls these APIs because they are just that: APIs. They are application programming interfaces that allow developers who are already using an existing NoSQL database technology to migrate to Cosmos DB without having to change their code.

Another huge advantage to Cosmos DB is a feature known as turnkey global distribution. This feature takes advantage of the horizontal scalability of NoSQL databases and allows you to replicate your data globally with a few clicks.

## Azure SQL Database

<img src="https://e7.pngegg.com/pngimages/170/924/png-clipart-microsoft-sql-server-microsoft-azure-sql-database-microsoft-text-logo-thumbnail.png" alt="Azure SQL Database" width="50">

Azure SQL Database is a PaaS offering for the SQL Server database. Azure offers three different deployment options for Azure SQL database:

### Single Database

A single database represents simply a database that is running on a sql server. Azure manages the database server, but the customer needs to manage the database. Azure provides two different purchase models for single databases: Database Transaction Unit (DTU) and virtual core (vCore).

DTU represents a collection of CPU, memory, and data reads and writes that come in three tiers: Basic, Standard, and Premium.

vCore represents a more granular configuration, being able to choose the exact hardware you need.

|      DTU    Model                                                                                                                   |      vCore    Model                                                                                                                                            |   |
|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
|     Good choice for users who don’t   need a high degree of flexibility with configuration and who want fixed   pricing.            |     Good choice if you need a high   level of visibility and control of individual resources (such as memory,   storage, and CPU power) your database uses.    |   |
|     Pre-configured limits for   transactions against the database, and pre-configured storage, CPU, and   memory configurations.    |     Flexibility in CPU power, memory,   and storage, with storage charged on a usage basis.                                                                    |   |
|     Basic and Standard offerings,   along with a Premium tier for production databases with a large number of   transactions.       |     General Purpose and Business   Critical offerings to provide lower costs when desired and high-performance   and availability when required.               |   |
|     Ability to scale to a higher tier   when needed.                                                                                |     Ability and flexibility to scale   CPU, memory, and storage as needed.                                                                                     |   |
|     Backup storage and long-term   retention of data provided for an additional charge.                                             |     Backup storage and long-term   retention of data provided for an additional charge.                                                                        |   |

### Elastic pool

This model consists of more than one databases managed by the same SQL server. This offering is more geared towards SaaS applications, where each user could have its own database, and moving databases in and out of an elastic pool is easily done.

In this case, you are charged for the resources used by the entire pool, not by single databases.

### Managed instance

This model is designed for customers that want to migrated from on-premises or another non-azure environment to Azure.

Azure developed a tool called Azure Database Migration Service (DMS) to make it easier for customers to move on-premises databases to a managed instance.

## Azure Database for MySQL

<img src="https://daporo.gallerycdn.vsassets.io/extensions/daporo/mysql-toolkit-win/0.0.2/1517180511799/Microsoft.VisualStudio.Services.Icons.Default" alt="Azure MySQL" width="50">

Azure Database for MySQL is a relational open-source database system. Since it is based on the MySQL Community Edition, you can easily move on-premises MySQL databases to the Azure cloud.

It offers several pricing plans based on your needs:

- **Basic**: light usage
- **General-Purpose**: business use
- **Memory Optimized**: high-performance requirements

## Azure Database for PostgreSQL

<img src="https://gravitydata.co/wp-content/uploads/2021/06/Azure-DB-for-Postgres.png" alt="Azure PostgreSQL" width="50">

Azure Database for PostgreSQL is a relational open-source database system. The pricing model is similar to Azure database for MySQL. The Azure cloud manages the server, database security, performance, and other administrative tasks.
