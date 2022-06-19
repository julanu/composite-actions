## composite-actions 
Repository containing multiple composite Github Actions(multiple declared in a YML which will evaluate to a single Github Action) for CI/CD pipelines.


<br/>

### Available composite actions:
- Docker Build & Push Image to DockerHub

<br/>

### Usage:
```yaml
  # Login, build and push Docker image to DockerHub
  - name: Build and Push the image
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
