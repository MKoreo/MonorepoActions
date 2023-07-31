# Github Action: mkoreo/pnpm-filter@v1
This Github action sets up PNPM and makes use of the "pnpm --filter" command to determine if the source code of an app/service has changed, compared to a pull request (PR) being made.
This includes detection of changes to the monorepo packages, which are defined as dependencies of the app/service in package.json.

# Usage
Use the github action by calling the external repo github action: "mkoreo/pnpm-filter@v1"
Define input parameters:
- PAT: The PAT for your github repository, to checkout the source code and pull request.

Use output parameter:
- changedProjects: List of projectfolder names that have changed.

Example usage in workflow:
```
    steps:
    steps:
    - id: pnpm-filter
      uses: mkoreo/pnpm-filter@v1
      with:
        PAT: ${{secrets.PAT}}

    - name: Build
    if: contains( steps.pnpm-filter.outputs.changedProjects , 'auth-service')
    uses: docker/build-push-action@v4
    with:
      file: ./projects/backend/auth-service/Dockerfile
      target: test-target
      cache-from: type=gha
      cache-to: type=gha,mode=max
      context: .
```
