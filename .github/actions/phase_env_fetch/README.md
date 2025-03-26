# Fetch Phase Secrets

Fetches secrets from Phase and generates a .env file.

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `phase_service_token` | Yes | - | Service token for authenticating with the Phase CLI |
| `phase_app_id` | Yes | - | Application ID to fetch secrets from in Phase |
| `phase_env` | Yes | - | Environment name to fetch secrets for |
| `phase_host` | No | - | Custom Phase host URL for self-hosted instances |
| `output_file` | No | `.env` | Path where the .env file will be written |
| `secrets_to_fetch` | No | - | Space-separated list of specific secrets to fetch |

## Usage Example

```yaml
- name: Generate .env from Phase
  uses: naxa-developers/gh-workflows/.github/actions/phase_env_fetch@phase_env_fetch/v1.0.0
  with:
    phase_service_token: ${{ secrets.PHASE_SERVICE_TOKEN }}
    phase_app_id: ${{ env.PHASE_APP_ID }}
    phase_env: ${{ needs.build.outputs.branch }}
    phase_host: ${{ env.PHASE_HOST }}
```
> [!IMPORTANT]
> Compatible with ubuntu based runners only.