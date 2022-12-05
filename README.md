# Requirements
* TKG v1.5.1 or greater cluster

# Instructions  
First, install cert-manager. 
`tanzu package install cert-manager -p cert-manager.tanzu.vmware.com -v 1.5.3+vmware.2-tkg.1`

Next, create a namespace to hold the installs for this package:
`kubectl create ns waas-install`

Create a service account for the app definition to use:
`kubectl apply -f setup/rbac/service-account.yaml`

Copy setup/values-example.yaml to values.yaml, and edit for your install.  Then apply it to the cluster.
`kubectl create secret generic waas-install-values -n waas-install --from-file=values.yaml`

Apply the App definition for kapp-controller to reconcile for us.
`kubectl apply -f setup/waas-install.yaml`

# Updating install settings
Apply changes to your cluster.
`kubectl create secret generic waas-install-values -n waas-install --from-file=values.yaml --dry-run=client -o yaml | kubectl apply -f-`
