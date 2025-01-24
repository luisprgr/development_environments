# Development Environments

This repository contains my containerized development environments, which can run in:

- [x] Toolbox  
- [x] Distrobox (Theoretically compatible, but not yet tested)  

The goal of this repository is to:

- Save time by avoiding the need to manually install each tool required for specific tasks
- Have all the tools I need with a single command
- Update tools easily without the risk of breaking system dependencies
- Maintain version control for some configurations

## Environments and Tools Included  

### DevOps  
  - [x] Terraform
  - [x] [Tenv](https://github.com/tofuutils/tenv) 
  - [x] AWS CLI
  - [ ] Semgrep
  - [ ] Kubectl

## Running in Toolbox

### Requirements:

- Podman (usually preinstalled with Toolbox)

### Local Build

#### Create an image that can be used in Toolbox using the Dockerfile

```bash
podman build -t devops-image .
```

#### Create a Toolbox container using the image

```bash
toolbox create --image devops-image DevOps
```

#### Enter the Toolbox

```bash
toolbox enter DevOps
```
