# gitlab-lke-k8s
config for managing k8s on Linode through Gitlab

The purpose of this project is to provide a template for managing k8s clusters through CI/CD on Gitlab.

Pre-requisites:  
You must have a Gitlab account with access to a Docker runner.
You should have already created your k8s cluster through your CSP using whatever method you choose.
You should have access to a bastion with kubectl and helm
KAS should be running on your server (ignore this for Gitlab.com)
Infrastructure must be enabled on the project.

Steps:
Fork this repo.
Create a Personal Access Token in your Github account.
Import this project into your Gitlab (you must use the same email address on both Gitlab and Github).
Determine the structure you want to use.  This setup uses /us-east /us-west to hold yamls for each cluster.
The example agent files are set up in the following manner and you should change a few fields:
  Within .gitlab/agents/us-east-prod/config.yaml 
 Modify the config:
  On line 3 modify the project path to suit your own project path from your browser bar.
  On line 4 set the default namespace you would like to work with in the k8s cluster.  This is where your yamls will default to if you do not specify a namespace in the yaml
  On line 6 set the path to monitor for changes.
    This example shows /us-east-prod/*.{yaml,json,yml}_ so our agent will look for any yaml, yml or json file extensions in that /us-east-prod/ directory at the root of our project
  Commit your changes.
  Click on Infrastructure in the left navigation and select Kubernetes.
  Click Connect cluster and select the agent you just modified.
  This will spit out a helm chart that must be run against the cluster.
    If you are working with multiple clusters, you must also declare the --kubeconfig= line to tell helm with cluster you are modifying
   
  
