--------------------------------------
SDP Generic k8s Deployment Helm Chart
--------------------------------------
## Pre-requisites

helm package manager (with helm and tiller components) must be installed and functional 
(This chart has been tested with helm version 2.16.1 and is not been tested with versions above 2.16.1 or with Helm 3)

### Create ImagePullSecret for GitHub
GitHub Docker Packages requires valid GitHub credentials to pull images. Generate an OAuth token for a valid GitHub user. Preferrably, this will be a service account that isn't tied to a specific team member.

Run the following command, changing the values to your GitHub credentails:

```bash
kubectl create secret docker-registry github --docker-server=https://docker.pkg.github.com \
--docker-username=${GITHUB_USER} --docker-password=${GITHUB_OAUTH_TOKEN}
```

## Chart Details

This chart will do the following:

* Install a Jenkins Master in the default namespace
* Optionally install persistent Jenkins agents
* Optionally install sonarqube server


## Installing the Chart

Note: Customize values.yaml for sdp sdp-jenkins sdp-sonarqube based on the target deployment environment 

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release sdp/
```

To uninstall the chart with the release name `my-release`:

```bash
$ helm delete --purge  my-release 
$ kubectl delete secret sdp-jenkins-secret
```


## Configuration

The following tables list the configurable parameters of the Jenkins chart and their default values. The chart can be customized by modifying these values.

### Jenkins Master

| Parameter                         | Description                          | Default                                   |
| --------------------------------- | ------------------------------------ | ----------------------------------------- |
| `sdp-jenkins.persistentSlaveEnabled`          | Deploy persistent Jenkins agents     | `true`                                    |
| `sdp-jenkins.numAgents `                     | Number of Agents to be deployed      | `1`                                       |
| `sdp-sonarqube.enabled`                    | Deploy Sonarqube  | `true`                                 |

