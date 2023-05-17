# gitlab-lke-k8s

The purpose of this project is to provide a template for managing LKE (k8s) clusters through Gitlab.

**Pre-requisites:**  
You must have a Gitlab account.  
You should have already created your k8s cluster through your CSP (Akamai) using whatever method you choose.  
You should have access to a bastion with kubectl and helm.  
KAS should be running on your server (ignore this for Gitlab.com).  
Infrastructure must be enabled on the project.  

**Steps:**  
- Fork this repo.  
- Create a Personal Access Token in your Github account.  
- Import this project into your Gitlab (you must use the same email address on both Gitlab and Github).  
- Determine the structure you want to use.  This setup uses /us-east /us-west to hold yamls for each cluster.  
- The example agent files are set up in the following manner and you should change a few fields:  
- Within .gitlab/agents/us-east-prod/config.yaml 
- Modify the config:
```  
On line 3 modify the project path to suit your own project path from your browser bar.  
On line 4 set the default namespace you would like to work with in the k8s cluster.  This is where your yamls will default to if you do not specify a namespace in the yaml
On line 6 set the path to monitor for changes.  

The example in this project shows /us-east-prod/*.{yaml,json,yml}_ so our agent will look for any yaml, yml or json file extensions in that /us-east-prod/ directory at the root of our project  
```
- Commit your changes.  
- Click on Infrastructure in the left navigation and select Kubernetes.  
- Click Connect cluster and select the agent you just modified. 
``` 
This will spit out a helm chart that must be run against the cluster.  
```
- From a console with Helm installed, run the helm chart as speficied in the output generated by Gitlab.  
```
If you are working with multiple clusters, you must also declare the --kubeconfig [path] line to tell helm which cluster you are modifying
```  
- Once the helm chart is run against the cluster, it will spin up the Pod that interfaces with KAS.  
**WARNING**  Any YAMLs in the PATHs specified in the config.yaml file of the agent will be executed immediately when the cluster connects.  
**WARNING**  Some sample yamls are included under the east and west directories.  These YAMLs will spin up an nginx replica set and cloud load balancer in each k8s cluster.  
- Edit these files or add new yamls to support your k8s deployments
   
  
