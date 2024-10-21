[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0

## Training Program
1. Docker architecture fundamentals
- Containers and Virtualization
- Namespaces and Control groups
- Labs
  - Test Docker installation
2. Containers
- Managing Containers
- Interacting with Running Containers
- Labs
  - List Docker containers
  - Start and Stop
  - Detached vs Interactive
  - Docker system 
3. Images
- Image filesystem
- Dockerfile
- Building Container Images
- Labs
  - Share Docker image
  - Create image using commit
  - Create image using dockerfile
  - Multi-stage dockerfile
4. Container Storage
- Data in containers
- Labs
  - Use Host mounted volume
  - Docker volume
5. Container Networking
- CNM Model
- Labs
  - Publish Ports
  - User-defined bridge networks
6. Resources
- Resource constraints
- Labs
  - Limit a container's resources (CPU/Memory)
7. container logs
- Logging drivers
- Labs
  - Container logs
  
## Optional Bonus
8. security
9. registry
10. rest api


## Labs

Install Docker Engine.

For more details :[Docker Site] https://docs.docker.com/engine/install/

Are you ready. Now, go Labs :)

To download the labs you can use the following command
```
scp -i key.pem -r ubuntu@myip:/home/ubuntu/DockerFundamentalsLabs-v1.5.0/ "$(pwd)"
```
```# DockerFundamentalsLabs-v1.5.0
