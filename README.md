## composite-actions - not perfect but alright
Repository containing multiple composite Github Actions(multiple declared in a YML which will evaluate to a single Github Action) for CI/CD pipelines.
<br/>

## Usage of available composite actions:
Look for for the latest version available on the [Releases](https://github.com/julanu/composite-actions/releases) page of this repository and update the actions `@version`.


### 1. Docker Build & Push Image to DockerHub
> [!NOTE]  
> This template assumes Docker is already installed on the agent
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
> [!NOTE]  
> This template assumes the agent running it is already logged in to Azure and has the necessary permissions setup to deploy
```yaml
  # Add Helm repository, update repository, dry-run and install
  - name: Helm Deploy to Kubernetes
    uses: julanu/composite-actions/helm-deploy@latest
    with:
      chart_name: my-chart
      registry_url: https://charts.helm.sh/stable
      registry_name: bitnami
      namespace: testing
      chart_version: 4.1.14
      helm_values_file: values.yaml
```
### 3. Terraform Plan & Apply
> [!NOTE]  
> This Terraform template will run apply on any branch and doesn't support a lot of parameters that can be provided to Terraform CLI 
```yaml
  # Initialize, Validate, Plan and Apply 
  - name: Terraform
    uses: julanu/composite-actions/terraform-cli-deploy@latest
    with:
      initArguments: "-reconfigure"
      additionalArguments: "-var-file=env/devel.tfvars -no-color"
      working-directory: "infra/"
``` 
### 4. Create Version Tag
> [!NOTE]  
> This will create a semver-like tag based on the latest one, differing for main and other branches
```yaml
  # Checkout and create a new version tag
  - name: Create Version Tag
    uses: julanu/composite-actions/create-version-tag@latest
    with:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```