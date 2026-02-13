# Build Docker Image (Composite Action)

Builds and pushes a Docker image to **AWS ECR**.  
Optionally fetches environment variables from **Phase** (if required for frontend builds).

## What it does

- Checks out your repository at the provided branch
- Optionally copies dependency files as:
  - `apt_requirements.txt`
  - `requirements.txt`
- Configures AWS credentials
- Logs in to Amazon ECR
- (Optional) Fetches secrets/env from Phase and generates `.env` (depends on `phase_env_fetch` action behavior)
- Builds and pushes Docker image to ECR using Docker Buildx
- Uses registry-based build cache (`:buildcache`) for faster builds

## Inputs

### Required

| Name | Description |
|------|------------|
| `AWS_ACCESS_KEY_ID` | AWS access key |
| `AWS_SECRET_ACCESS_KEY` | AWS secret key |
| `AWS_REGION` | AWS region |
| `BRANCH_NAME` | Branch name to checkout |
| `ECR_REGISTRY` | ECR registry URL (e.g. `123456789012.dkr.ecr.ap-south-1.amazonaws.com`) |
| `ECR_REPOSITORY` | ECR repository name |


### Optional

| Name | Default | Description |
|------|---------|------------|
| `DOCKERFILE_PATH` | `./docker/Dockerfile` | Path to Dockerfile |
| `BUILD_CONTEXT` | `.` | Docker build context |
| `PIP_MODULES_FILE` | `./dependencies/requirements_gis.txt` | If file exists, copied to `requirements.txt` |
| `APT_MODULES_FILE` | `./dependencies/apt_requirements_gis.txt` | If file exists, copied to `apt_requirements.txt` |
| `IMAGE_TAG` | _(branch name)_ | Image tag; if empty uses `BRANCH_NAME` |
| `ENABLE_PHASE_ENV_FETCH` | `"false"` | Set `"true"` to run Phase env fetch |
| `PHASE_APP_ID` | Phase app/project id | ID of phase app
| `PHASE_SERVICE_TOKEN` | - | Phase service token |
| `PHASE_HOST` | `https://phase.naxa.com.np` | Phase host URL |
| `PHASE_ENV` | - | Phase environment name (`develop`, `staging`, `master`, etc.) |

## How to Use ?

### Backend (skip Phase env fetch)

```yaml
- name: Build & Push Backend Image
  uses: naxa-developers/gh-workflows/.github/actions/build_and_push@master
  with:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    AWS_REGION: ap-south-1
    BRANCH_NAME: ${{ github.ref_name }}
    ECR_REGISTRY: ${{ secrets.ECR_REGISTRY }}
    ECR_REPOSITORY: backend
    ENABLE_PHASE_ENV_FETCH: "false"
    PHASE_APP_ID: "dummy-or-required-by-action"
````

### Frontend (enable Phase env fetch)

```yaml
- name: Build & Push Frontend Image
  uses: naxa-developers/gh-workflows/.github/actions/build_and_push@master
  with:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    AWS_REGION: ap-south-1
    BRANCH_NAME: ${{ github.ref_name }}
    ECR_REGISTRY: ${{ secrets.ECR_REGISTRY }}
    ECR_REPOSITORY: frontend
    IMAGE_TAG: ${{ github.ref_name }}
    ENABLE_PHASE_ENV_FETCH: "true"
    PHASE_SERVICE_TOKEN: ${{ secrets.PHASE_SERVICE_TOKEN }}
    PHASE_APP_ID: ${{ secrets.PHASE_APP_ID }}
    PHASE_ENV: develop
    PHASE_HOST: https://phase.naxa.com.np
```