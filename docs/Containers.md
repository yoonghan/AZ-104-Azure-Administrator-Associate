# Containers
**NOTE:** Virtual machines provide a complete isolation and strong security boundaries than containers.
![Container Instance](https://learn.microsoft.com/en-us/azure/container-instances/)

## Azure Container Registry
Like Docker Hub, but private.

## Azure Container Instance

### Just Instance
1. Custom sizes. You specify CPU cores (from 0.1 to 4 vCPU) and memory (from 0.1 to 16 GB) for each container at deployment time. Resource allocation is fixed for the lifetime of the container group.
2. Persistent storage. Containers support direct mounting of Azure Files file shares.
![Container Instance](img/container-instance.png.png)

### Container Group
1. A container group is a collection of containers that get scheduled on the same host machine. The containers in a container group share a lifecycle, resources, local network, and storage volumes. It's similar in concept to a pod in Kubernetes.
2. Configured using a YAML or ARM template.
3. Can be scheduled on a single host machine.
4. Can be assigned a DNS name label.
5. Can expose a single public IP address, with one exposed port.
6. Can consist of multiple containers. One container listens on port 80, while the other listens on port 5000.
7. Can include multiple Azure file shares as volume mounts, and each container mounts one of the shares locally.
8. Example:Create a multi-container group to hold your **front-end container** and **back-end container**. The front-end container can serve a web app. The back-end container can run a service to retrieve data.

![Container Group](img/containerinstance_container_group.png)

## Azure Container Apps
1. Azure Container Apps is a serverless platform that allows you to maintain less infrastructure and save costs while running containerized applications. Instead of worrying about server configuration, container orchestration, and deployment details, Container Apps provides all the up-to-date server resources required to keep your applications stable and secure.
2. Common uses of Azure Container Apps include:
    - Deploying API endpoints
    - Hosting background processing jobs
    - Handling event-driven processing
    - Running microservices
3. Applications built on Azure Container Apps can dynamically scale based on the following characteristics:
    - HTTP traffic
    - Event-driven processing
    - CPU or memory load
    - Any KEDA-supported scaler
4. Azure Container Apps doesn't provide direct access to the underlying Kubernetes APIs. Though powered by Kubernetes and open-source technologies like Dapr, KEDA, and envoy.

![Container Apps](img/containerapps.png)

## Azure Kubernetes Service

| Feature | Azure Container Apps (ACA) | Azure Kubernetes Service (AKS)
| --- | --- | --- |
| Overview | ACA is a serverless container platform that simplifies the deployment and management of microservices-based applications by abstracting away the underlying infrastructure. | AKS simplifies deploying a managed Kubernetes cluster in Azure by offloading the operational overhead to Azure. It’s suitable for complex applications that require orchestration. |
| Deployment | ACA provides a PaaS experience with quick deployment and management capabilities. | AKS offers more control and customization options for Kubernetes environments, making it suitable for complex applications and microservices. |
| Management | ACA builds upon AKS and offers a simplified PaaS experience for running containers. | AKS provides a more granular control over the Kubernetes environment, suitable for teams with Kubernetes expertise. |
| Scalability | ACA supports both HTTP-based autoscaling and event-driven scaling, making it ideal for applications that need to respond quickly to changes in demand. | AKS offers horizontal pod autoscaling and cluster autoscaling, providing robust scalability options for containerized applications. |
| Use Cases | ACA is designed for microservices and serverless applications that benefit from rapid scaling and simplified management. | AKS is best for complex, long-running applications. These applications require full Kubernetes features and tight integration with other Azure services. |


## Container management
1. Azure Container Instances (ACI) is best for isolated, short-lived tasks. 
2. Azure Container Apps (ACA) serves serverless microservices. 
3. Azure Kubernetes Service (AKS) provides full Kubernetes control for complex orchestration needs.

