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
