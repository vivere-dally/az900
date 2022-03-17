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

<img src="https://wedoazure.files.wordpress.com/2019/08/image-27.png" alt="Network Security Group" width="50">

## Azure VPN Gateway

<img src="https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/images/vpn.png" alt="VPN Gateway" width="1000">

A VPN Gateway is used in cases where two or more VNets need to communicate, or if you want a VNet to communicate with on-premise resources. The traffic will travel over the internet, so to add a layer o security for the network traffic, you can use a virtual private network (VPN) connection.

Azure VPN Gateway uses VPN connections to enable secure connectivity between Azure VNets and other networks. It uses Internet protocol security (IPSec) and the Internet key exchange (IKE) protocols.

The VPN Gateway is running on top of two or more VMs that are created inside a subnet. They are created explicitly for the VPN Gateway and you cannot remote into them or change their configurations.

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

## Azure Cosmos DB

<img src="https://gotcosmos.com/images/about/cosmos-logo.svg?v=TV8GAN6U90A78jwat9z4a3cLY6dIphJm8XyfL_NkOjw" alt="Azure Cosmos DB" width="50">
