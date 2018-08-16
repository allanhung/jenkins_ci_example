# github integration with jenkins

This repository will show you how to integration github and jenkins.

## Run Jenkins

Run the jenkinsci/blueocean image as a container
```bash
docker run \
  --rm \
  --name jenkins \
  -u root \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins-data:/var/jenkins_home \ 
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkinsci/blueocean
```

## Generate github access token
github --> setting --> Personal Access Token --> Generate new token
```bash
select
  - repo
  - admin:repo_hook
  - user:email
```

## Create your Pipeline project in Blue Ocean

## Reference
  * https://jenkins.io/doc/tutorials/build-a-multibranch-pipeline-project
