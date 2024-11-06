#### For SSM actor based permissions

> Write given content to file. Ex: `input.json`
```json
{
    "use_default": false,
    "include_claim_keys": ["repo", "context", "actor"]
}
```

> Then call PUT API on github to send actor context too on `sub` claim field.
```sh
gh api -X PUT repos/naxa-developers/oidc-test/actions/oidc/customization/sub --input input.json
```

> Verify changes with
```sh
gh api -X GET repos/naxa-developers/oidc-test/actions/oidc/customization/sub
```
