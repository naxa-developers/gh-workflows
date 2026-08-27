# Build Artifact Uploader

Zips and uploads the build artifact to S3.

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `aws-role-arn` | Yes | - | IAM Role ARN to assume via GitHub OIDC |
| `aws-region` | Yes | `ap-south-1` | AWS region |
| `project-name` | Yes | - | Name of the project |
| `s3-base-path` | Yes | - | Base S3 path for uploads |
| `source-directory` | No | `dist` | Directory to zip and upload |

## Usage Example

```yaml
- name: Upload Build Artifacts
        uses: naxa-developers/gh-workflows/.github/actions/build-artifact-uploader@artifact_uploader/v1.0.0
        with:
          aws-role-arn: ${{ secrets.AWS_ROLE_ARN }}
          aws-region: ${{ env.AWS_REGION }}
          project-name: ${{ env.PROJECT_NAME }}
          s3-base-path: "s3://naxa-ci-artifacts"
          source-directory: "./dist"
```