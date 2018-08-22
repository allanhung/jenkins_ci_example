# github integration with jenkins

This repository will show you how to integration github and jenkins.

![alt text](https://github.com/allanhung/jenkins_ci_example/raw/master/jenkins_workflow.png "jenkins workflow")

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

Example to build plugin for jenkins
```bash
mkdir plugin_build && git clone https://github.com/AngryBytes/jenkins-build-everything-strategy-plugin
cd plugin_build/jenkins-build-everything-strategy-plugin
docker run -it --rm --name my-maven-project -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven maven:3.3-jdk-8 mvn package
cp target/build-everything-strategy.hpi ../../jenkins-data/plugins
```

Example restart jenkins
```bash
http://xxx/safeRestart
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
* Fork and clone this sample repository on github
* Create a new pipeline with blueocean pipeline creation wizard.

## Reference
  * https://jenkins.io/doc/tutorials/build-a-multibranch-pipeline-project
