# Week 4 - Virtualization and Containers
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

## What I Learned
This week focused on virtualized isolation, Docker containers, network segmentation, and multi-container application deployment. The work connected container operations to defense in depth because isolated networks and disposable environments reduce the risk of malware spread and service exposure.

## Artifacts
**docker-compose.yml**  
This artifact defines a WordPress and MySQL deployment using separate frontend and backend networks, with the backend network marked internal. It demonstrates service separation and network isolation in a containerized architecture.

**sandbox_report.txt**  
This report explains why a host-only sandbox blocks internet connectivity and why a SOC analyst should avoid bridged mode when detonating unknown malware. It connects virtualization settings to containment and safety.

**deploy_web.sh**  
This script deploys an nginx container in detached mode and maps the host port to the container web service. It demonstrates basic Docker command usage for repeatable web server deployment.

**hyper_stack/docker-compose.yml**  
This TLAB artifact defines a MariaDB and WordPress stack using public and private Docker networks. The database uses persistent storage, while the private network limits direct external exposure.

**hyper_stack/hyperstack_audit.json**  
This TLAB audit file records operator, host IP, VM sandbox IP, container ID, isolation status, and persistence verification. It confirms that the containerized environment was tested and documented.

## Challenges & How I Solved Them
The main challenge was understanding how network modes and Docker networks change exposure. I worked through this by comparing host-only sandbox behavior with container network segmentation and documenting whether isolation tests passed.

## Reflection
This week helped me see containers as both deployment tools and security boundaries. In future work, I would avoid hard-coded secrets in compose files and use environment files or secret management.

## References
Docker Inc. (2024). *Docker documentation*. https://docs.docker.com  
Oracle. (2024). *Oracle VM VirtualBox user manual*. https://www.virtualbox.org/manual/
