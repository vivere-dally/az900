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

<img src="https://w1.pngwing.com/pngs/652/487/png-transparent-sql-server-logo-kubernetes-microsoft-azure-docker-amazon-web-services-cloud-computing-high-availability-orchestration.png" alt="AKS" width="150">
