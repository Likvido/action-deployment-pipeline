# Unified Likvido github action for building and releasing apps

```
name: "App Name"

on:
  push:
    branches:
      - develop
      - master
    paths:
    - "<add all of the paths>"
  pull_request:
    branches:
      - develop
      - master
    paths:
    - "<add all of the paths again>"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Unified Build & Deploy
      uses: likvido/action-deployment-pipeline@v3.2
      with:
        staging-branch-name: develop
        production-branch-name: master
        pull-request-dockerfile-target: build
        docker-working-directory: src
        dockerfile-relative-path: Likvido.AccountingDebtorDeletedProcessor/Dockerfile
        deployment-path: src/Likvido.AccountingDebtorDeletedProcessor/deployment.yml
        app-name: accounting-debtor-deleted-processor
        kubernetes-namespace: default
        azure-service-principal-id: ${{ secrets.AZURE_SERVICE_PRINCIPAL_ID }}
        azure-service-principal-password: ${{ secrets.AZURE_SERVICE_PRINCIPAL_PASSWORD }}
```


# Releasing new version

Either create the new release + new version tag directly in the Github UI, or create it like this:

1. Commit and push your changes
2. Create a new tag: `git tag -a -m "Description of this release" <version>`
3. Push the tag: `git push --follow-tags`

## Example

```
git tag -a -m "First version" v1
git push --follow-tags
```
