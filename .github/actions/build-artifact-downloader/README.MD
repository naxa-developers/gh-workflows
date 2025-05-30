# Build Artifact Downloader

Downloads and extracts build artifacts from S3.

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `aws-access-key-id` | Yes | - | AWS access key ID |
| `aws-secret-access-key` | Yes | - | AWS secret access key |
| `aws-region` | Yes | `ap-south-1` | AWS region |
| `project-name` | Yes | - | Name of the project used during upload |
| `s3-base-path` | Yes | - | Base S3 path used during upload |
| `target-directory` | No | `./dist` | Directory to extract the artifact |

## Usage Example

```yaml
- name: Download Build Artifacts
        uses: naxa-developers/gh-workflows/.github/actions/build-artifact-downloader@artifact_downloader/v1.0.1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}
          project-name: ${{ env.PROJECT_NAME }}
          s3-base-path: "s3://naxa-ci-artifacts"
          target-directory: "./dist"
```