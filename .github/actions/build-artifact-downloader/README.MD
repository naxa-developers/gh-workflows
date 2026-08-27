# Build Artifact Downloader

Downloads and extracts build artifacts from S3.

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `aws-role-arn` | Yes | - | IAM Role ARN to assume via GitHub OIDC |
| `aws-region` | Yes | `ap-south-1` | AWS region |
| `project-name` | Yes | - | Name of the project used during upload |
| `s3-base-path` | Yes | - | Base S3 path used during upload |
| `target-directory` | No | `./dist` | Directory to extract the artifact |

## Usage Example

```yaml
- name: Download Build Artifacts
        uses: naxa-developers/gh-workflows/.github/actions/build-artifact-downloader@artifact_downloader/v1.0.1
        with:
          aws-role-arn: ${{ secrets.AWS_ROLE_ARN }}
          aws-region: ${{ env.AWS_REGION }}
          project-name: ${{ env.PROJECT_NAME }}
          s3-base-path: "s3://naxa-ci-artifacts"
          target-directory: "./dist"
```