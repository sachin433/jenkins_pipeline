Jenkins Dynamic slave can deploy directly into Kubernetes or Openshift CLuster provided we install "Kubernetes Continuous Deploy" plugin.

After installing, In the Jenkins Job configuration select "Deploy to Kubernetes" from "Build Step".
We can pass Kubeconfig file directly as Global Credential or SSH into Master node(wherein it will automcatically pick ~/kube/config file).

After passing SSH server and Credentials,Provide path of Config path of files to be deployed in the cluster.Place Config files in SCM and mention its location here:

for ex: Config Files= kubernetes_continuous_deploy/*.yaml

Check "Enable Variable Substitution in Config"

Provide "Docker Container Registry Credentials" if image has to pulled from private repository

Declarative Pipeline script for above fuctioanlity will be as follows:

kubernetesDeploy configs: 'kubernetes_continuous_deploy/*.yaml', credentialsType: 'SSH', kubeConfig: [path: ''], kubeconfigId: '', secretName: '', ssh: [sshCredentialsId: 'c1a63fa6-bc75-45be-938a-f7a7590a1a60', sshServer: 'xx.xx.xx.xx'], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
