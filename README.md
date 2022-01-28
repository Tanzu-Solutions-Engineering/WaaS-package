kubectl create ns waas-install

kubectl apply -f setup/rbac/service-account.yaml

tanzu package repository add cdelashmutt-repository \
  --url ghcr.io/cdelashmutt-pivotal/packagerepo:1.0.0 \
  --namespace waas-install

Copy setup/values-example.yaml to values.yaml, and edit for your install.

kubectl create secret generic waas-install-values -n waas-install --from-file=values.yaml

kubectl apply -f setup/waas-install.yaml