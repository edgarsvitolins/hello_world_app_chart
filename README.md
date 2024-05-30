### Description

Defines helm `hello-chart`

Runs two services - Spring Boot `backend`, and Django `frontend`, from images
>https://hub.docker.com/r/edgarsvitolins/hello_world_app<br>
> https://hub.docker.com/r/edgarsvitolins/hello_world_app_fe

which are defined in

>https://github.com/edgarsvitolins/hello_world_app<br>
>https://github.com/edgarsvitolins/hello_world_app_fe

### Different environments
Includes values for each of testing, staging, and prod environments in
```
hello-chart/values-testing.yml
hello-chart/values-satging.yml
hello-chart/values-prod.yml
```
### How to run
To run, for example, testing version on minikube, use
```
1. helm install hello-chart -f hello-chart/values-testing.yml ./hello-chart
2. minicube service frontend
```
which should display
```
Django FE presents: Hello from Spring Boot BE!
```

### Additional ideas
>1. `frontend` and `backend` unit tests when building docker images, checked in a stage in CI workflow
>2. Integration/acceptance tests
>3. Replace frontend with a production level server (instead of using the django built-in development server)
>4. Push helm chart to a hub (same as `frontend` and `backend` images are pushed to docker hub)
>5. Deploy to kubernetes cluster, for example AKS, using github workflows<br><br>Auto deploy to testing cluster on every change to either frontend or backend<br><br>Manually deploy using workflow to staging (must pass integration/acceptance tests)<br><br>Manually deploy to prod (must pass integration/acceptance tests)<br><br>Different image versions for testing vs staging/prod, where testing includes debug log info, etc<br><br>
>6. Protection rules to main branches
>7. Internal documentation for the available `backend` endpoints (currently only the default endpoint with greeting)
>8. Move hardcoded values, for example, env variable REACT_APP_BE_URI, to some config file

### Resources
Hello world app:
https://spring.io/guides/gs/spring-boot

Build jar in github workflow:
https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven

Building and pushing docker image to docker hub:
https://docs.github.com/en/actions/publishing-packages/publishing-docker-images

Kubernetes FE and BE:
https://kubernetes.io/docs/tasks/access-application-cluster/connecting-frontend-backend/

Deploying to AKS (automatically for testing/staging):
https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-to-azure-kubernetes-service

Manually running a workflow (to deploy to prod):
https://docs.github.com/en/actions/using-workflows/manually-running-a-workflow

Branch protection:
https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule
