# ITSA-5501 Project

Milestone 1: DevOps & System Integration

## Repository Structure
ITSA-5501-Project/
├── docker/ # Container images (Dockerfiles, scripts)
├── k8s/ # Kubernetes manifests/helm values
├── iac/ # Infrastructure-as-Code (e.g., Terraform)
└── README.md


## Git Workflow (Branching → PR → Merge → Tagging)
1. **Initialize**: `git init`, create folders, `.gitignore`, first commit.
2. **Commit in small steps**: meaningful messages (present tense).
3. **Branch**: `git checkout -b experiment` for feature work.
4. **Work on branch**: add files/changes, `git add`, `git commit`.
5. **Sync**: `git push -u origin experiment`.
6. **Pull Request**: open PR on GitHub, request review, address feedback.
7. **Merge**: merge PR into `main`. Resolve conflicts if any.
8. **Update local**: `git checkout main && git pull origin main`.
9. **Tag Milestone**: `git tag -a v1.0 -m "Milestone 1 complete" && git push origin v1.0`.

## Tools Used
- **Git/GitHub** for version control & collaboration
- **Docker** for containerization
- **Kubernetes** for deployment manifests
- **Terraform** (or other IaC) for infrastructure provisioning

## How to Contribute (Future)
- Create a feature branch: `git checkout -b feature/<name>`
- Follow conventional commits: `feat: ...`, `fix: ...`, `docs: ...`
- Open a PR to `main`, pass checks, request review, then merge
- Tag releases with `vX.Y.Z`






## Milestone 2 – Docker & Multi-Container Setup


- `frontend/`
  - `index.html` – Static page describing a vacation destination.
- `docker/`
  - `docker-compose.yml` – Multi-container configuration for:
    - `frontend` (nginx) serving static HTML
    - `user-db` (MongoDB with `user_data` volume)
    - `product-db` (PostgreSQL with `product_data` volume)
    - `cache` (Redis)
    - `prometheus` (Prometheus monitoring)
- `prometheus.yml` – Prometheus configuration with a basic scrape job.

### Docker Workflow

 **Start all services** (from `docker` folder):
docker compose up -d


Check container status:
docker ps

Access services:
Frontend: http://localhost:9090
Prometheus: http://localhost:9091


Scale frontend to 3 instances:
docker compose up -d --scale frontend=3


Stop and remove containers:
docker compose down



## Milestone 3 – Kubernetes

- Created PVC `shared-logs-pvc` (ReadWriteOnce, 500Mi).
- Deployed `nginx-sidecar-deployment` with:
  - 5 replicas (scaled from 2).
  - Containers: `nginx-container` (nginx:1.21) and `sidecar-container` (busybox).
  - Shared PVC volume mounted at `/usr/share/nginx/html` and `/data`.
- Exposed via NodePort service `nginx-sidecar-service` on port 30080.
- Verified data sharing between containers by writing and reading `log.txt` in the shared volume.
- Cleaned up deployment, service and PVC after verification.


## Milestone 3 – Infrastructure as Code (Terraform on Azure)

- Used Azure CLI and Terraform CLI to provision infrastructure.
- Defined variables for:
  - `resource_group_name = pm3VMResourceGroup`
  - `location = eastus`
  - `vm_size = Standard_B1s`
  - `admin_username = azureuser`
- Implemented `main.tf` to create:
  - Resource group `pm3VMResourceGroup`
  - Virtual network `myVMVnet` and subnet `myVMSubnet`
  - Public IP `myVMPublicIP` (Standard SKU, Static)
  - Network interface `myVMNic`
  - Linux VM `myLinuxVM` (Ubuntu Server 18.04 LTS)
- Implemented `outputs.tf` to output:
  - `resource_group_id`
  - `vm_public_ip`
  - `vm_id`
- Terraform workflow followed:
  - `terraform init`, `terraform fmt`, `terraform validate`
  - `terraform plan`, `terraform apply`
  - `terraform state list` / `terraform state show`
  - `terraform destroy` for cleanup.
