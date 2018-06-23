# Development Environment setup

[![DevOps](https://img.shields.io/badge/%20DevOps-Automation-yellow.svg)]()  [![DevOps](https://img.shields.io/badge/%20GCP-Kubernetes/GKE-blue.svg)]()  [![DevOps](https://img.shields.io/badge/%20CI&CD-jenkins-green.svg)]()

Automation has been achieved for the development environment. Any changes will trigger an automated deployment to the development cluster on Google cloud / Kubernetes. The following has been done.

  - Development environment with ssl enabled hosted at (domain) 
  - Continous integration and Integration deployment pipeline configured for the development enviroment using Jenkins. 
  - Integrated a few automation scripts
  
  # Deployment!

  - Application hosted with kubenetes on GKE (Google Kubernetes Engine) in the development cluster.
  - Domain linked to a reserved IP address. 
  - Uisng NGINX ingress controller with a load balancer to route traffic. SSL has been configured for https traffic.
  - NGINX ingress controller installed in the cluster as a chart using Helm (k8s package manager)
  - K8s yaml files (deployment, service, ingress etc) have been included in the k8s folder in the home directory. 
 
 # CI & CD!

  - Using Jenkins as the continous integration and continous deployment tool.
  - Automated builds support, currently for develop branch. This would require adjusting the current development git workflow to make develop branch the only dependance for any deployment.
  - Merging to develop will trigger a build on Jenkins that will run the test and deploy jobs.
  - Environment variables have been set on the Jenkins dashboard.
  - A deploy.sh script containing the deployment commands has been integrated in the scripts folder in the home directory which is called by the Jenkinsfile to trigger the deployment.

# Automation!
The following has been automated through the CI&CD pipeline;
  - installing Google CloudSdk.
  - authenticating With Service Account.
  - configuring Google CloudSdk.
  - logging in to Container Registry.
  - building and tagging the docker image.
  - publishing the docker image.
  - logging out of the container registry.
  - deploying to the Kubernetes cluster.
  
  ### Commands used to implement development deployment

To create the service, deployment, ingress, namespace etc files in the k8s folder, we run the following command;

```sh
$ cd k8s
$ kubectl create filename.yml
```

And to update the service, deployment, namespace, run;

```sh
$ cd k8s
$ kubectl apply filename.yml
```

Note: It's recomended to first delete the ingress, make changes then recreate it again for the changes to be effectively integrated.

And to delete them, run;

```sh
$ cd k8s
$ kubectl delete filename.yml
```

### Recommendations 

 - Write MORE Tests as they are the back bone of CI & CD.
 - Changing git workflow, e.g branching off develop to build new features. Merging back to develop should trigger deployment to the development cluster for now. The staging branch could adopted as the application grows.
 - Integrating test coverage reports and system checks like coveralls and codeclimate. 
 - Higher level automation can be achieved by configuring scripts for e.g;
 automating the creation of clusters using terraform e.g staging and production environments.
Integrating feedback responses e.g slack notifications or emails for new deployments etc.
Automating renewal of ssl certificates as the surrent one is valid for 3 months.
 - Using Helm to create charts and manage releases for the project. This will enable installation of the application in another cluster easily.
 - Implement monitoring and logging to gather feedback and logs from the application easily. Used tools can be stackdriver, bugsnag or datadog etc.
 
 ### Contributors
  - David
