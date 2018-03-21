
**_Quick Note_**
- *You can run these plugins without having to use kubectl's "plugin" command at runtime. Just, "kubectl ssh, or kubectl deploy", for example.*
- *All coding was written to maintain compatibility across both BSD and GNU.*
- *The _"deploy"_ plugin contains some in-house customizations. You'll want to adjust accordingly if using it as a template for your own work.*
- *Also, any/all PRs for this readme file will be instantly and automatically merged, ;P*

# kubectl-plugins

A collection of plugins for kubectl integration
 - Some plugins Require jq ( brew/apt/yum install jq )

## Install on Linux/Mac
  Just run the install-plugins script and source your ~/.bash_profile!
  To remove, delete the ~/.kube/plugins folder and comment the entry (a one line kubectl function) in your bash_profile.
  
 ### kubectl ssh
 ![ssh](https://user-images.githubusercontent.com/22456127/37712530-90db197e-2cea-11e8-8e3a-ae871ce481aa.gif)
  - Like kubectl exec, but offers a --user flag to exec as root (or any other user)
  - 'ssh' is a misnomer (it works by mounting a docker socket as a volume), but it's easier to work with as a command.
  - Kudos to mikelorant for thinking of the docker socket! :)
  - Usage: kubectl ssh -u root zookeeper-1


### kubectl deploy [options]
![deploy](https://user-images.githubusercontent.com/22456127/36905632-d3f22eca-1e01-11e8-8d65-33dd556c8544.gif)

   [-f, --file] (Ex: -f 20-actions.yml) File to deploy. At this time, only accepts a single file. Required.
  
   [-i, --image] (Optional. Ex: -i kafka:v1.0.0 **or** -i kafka) Docker image/tag to use. Overwrites what's set in the manifest. If only the image name is passed, it displays a list of images to choose from. Optional.
  
   [-d, --dry] (Ex: -d true) Runs the command in dry-run mode. Optional.
  
   [-n, --namespace] (Ex: -n preprod) Namespace/Environment to deploy to (defaults to current ns). Optional
   
   Example: kubectl deploy -f 40-actions.yml -i actions -n staging


 ### kubectl switch [options]
 ![ssh](https://user-images.githubusercontent.com/22456127/37712867-84b950f6-2ceb-11e8-8959-289a6ff7a81e.gif)
  - View current namespace: kubectl switch
  - Switch namespace: kubectl switch preprod
  - Switch cluster: kubectl switch cluster staging (cluster switching requires the user add their project name in the switch.sh file).

### kubectl verify
  - Non-interactive plugin that prompts users before executing a create/apply/deploy/delete command in a production namespace.
  - If you do not want this, change your ~/.bash_profile and remove the first "case in" of the function mentioning it.


 ### kubectl get-node-ip
 ![get-node-ip](https://user-images.githubusercontent.com/22456127/36905626-d2652a9e-1e01-11e8-87a8-9942fd5b2307.gif)
  - Outputs the node location and IP for a given application e.g., kubectl get-nodes rabbitmq
  
  - Usage: kubectl get-node-ip (app or statefulset name...not the pod name)


 ### kubectl uptime
  - Displays total uptime for pods/statefulsets in the user namespace.
