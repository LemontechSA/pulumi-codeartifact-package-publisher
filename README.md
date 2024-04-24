# pulumi-codeartifact-package-publisher
A composite action for publishing Pulumi packages

_This Action is currently in preview and meant for internal use. Any functionality can and likely will change._

### Purpose
This Action automates setup and publication to the package registries of Python and NodeJS.

### Setup

Set the following steps and parameters in your workflow:

```yaml
steps:
  - name: Publish Python SDK
    uses: LemontechSA/pulumi-codeartifact-package-publisher@v0.0.2
    with:
      sdk: python
      aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      codeartifact_repository: ${{ vars.CODEARTIFACT_REPOSITORY }}
      codeartifact_domain: ${{ vars.CODEARTIFACT_DOMAIN }}
      codeartifact_domain_owner: ${{ vars.CODEARTIFACT_DOMAIN_OWNER }}
      codeartifact_region: ${{ vars.CODEARTIFACT_REGION }}
```

#### `with.sdk`

Optionally, you may specify language SDKs individually or in a comma separated list.

Valid inputs to `with.sdk` are:

- `all` - Equivalent to specifying all supported registries: `python,nodejs`
- `python` - Publish to PyPI
- `nodejs` - Publish to npm
- `!${LANG}` - To disable any of the above languages.

##### Examples

###### Use

Add this action to your workflow as a step to publish to Python and NPM registries:

```yaml
steps:
  - name: Publish all SDKs
    uses: LemontechSA/pulumu-codeartifact-package-publisher@v0.0.2
```

###### Publish the NodeJS SDK Only

```yaml
steps:
  - uses: LemontechSA/pulumu-codeartifact-package-publisher@v0.0.2
    with:
      sdk: nodejs
```
