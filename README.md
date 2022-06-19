## composite-actions - 
Repository containing multiple composite Github Actions(multiple declared in a YML which will evaluate to a single Github Action) for CI/CD pipelines.
<br/>

## Usage of available composite actions:
Look for for the latest version available on the [Releases](https://github.com/julanu/composite-actions/releases) page of this repository and update the actions `@version`.


### 1. Docker Build & Push Image to DockerHub
```yaml
  # Login, build and push Docker image to DockerHub
  - name: Build and Push Docker
    uses: julanu/composite-actions/docker-build-push@latest
    with:
      registry_user: userID
      registry_pwd: userToken
      image_name: repo/image
      tag: latest
      context: .
      dockerfile: ./Dockerfile
      platforms: linux/arm64,linux/amd64
      build_args: -e "token=value"
```
### 2. Deploy Helm chart to Kubernetes  
```yaml
  # Add Helm repository, update, dry-run and install
  - name: Helm Deploy to Kubernetes
    uses: julanu/composite-actions/helm-deploy@latest
    with:
      chart_name: my-chart
      registry_url: https://charts.helm.sh/stable
      registry_name: bitnami
      namespace: testing
      chart_version: 4.1.14
```
