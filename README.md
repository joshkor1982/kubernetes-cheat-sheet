# kubernetes-cheat-sheet
## CKA Kubernetes Command Cheat Sheet

#### Setting question context in CKA exam:
`kubectl config set-context <context-of-question> --namespace=<namespace-of-question>`

#### Set alias for kubectl:
`alias k=kubectl`

#### Find shortnames for resources:
`kubectl api-resources`

#### Immediate deletion of a resource:
`kubectl delete pod nginx --grace-period=0 --force`

#### Finding object information:
`kubectl describe pods | grep -C 10 "item to look for"`

or in yaml:
`kubectl get pods -o yaml | grep -C 5 labels:`

#### Using help for commands:
`kubectl delete --help`
`kubectl create --help`
`kubectl describe --help`

#### Get specific with describing objects:

`kubectl explain pod.spec`

#### What is RBAC?
 
`RBAC defines policies for users, groups, and processes by allowing or disallowing access to manage API resources.`
 
#### KUBERNETES AUTO-COMPLETION
`echo 'source <(kubectl completion bash)' >>~/.bashrc`

#### GET CLUSTERS
`kubectl get clusters`

#### GET NODES
`kubectl get nodes`

#### GET NAMESPACE
`kubectl get namespaces`

#### GET PODS IN A NAMESPACE
`kubectl get pods -n <namespace>`

#### CREATE A NAMESPACE
`kubectl create ns my-namespace`

#### DESCRIBE PODS IN A NAMESPACE
`kubectl describe pods <podname> -n <namespace>`

#### SWITCH CONTEXT TO A SPECIFIC NAMESPACE
`kubectl config set-context --current --namespace=my-namespace`

#### GET PODS BY LABELS AND SELECTORS (-l IS SHORT FOR SELECTOR)
`kubectl get pods -l app=name-of-app -A`

