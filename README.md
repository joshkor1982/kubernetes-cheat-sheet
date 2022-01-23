# kubernetes-cheat-sheet
## KUBERNETES (AND MORE) COMMAND CHEAT SHEET

#### SETTING QUESTION CONTEXT IN CKA EXAM:
`kubectl config set-context <context-of-question> --namespace=<namespace-of-question>`

#### SET ALIAS FOR KUBECTL:
`alias k=kubectl`

#### FIND SHORTNAMES FOR RESOURCES:
`kubectl api-resources`

#### IMMEDIATELY DELETE A RESOURCE:
`kubectl delete pod nginx --grace-period=0 --force`

#### FINDING OBJECT INFORMATION:
`kubectl describe pods | grep -C 10 "item to look for"`

#### OR IN YAML FORMAT:
`kubectl get pods -o yaml | grep -C 5 labels:`

#### USING HELP FOR COMMANDS:
`kubectl delete --help`
`kubectl create --help`
`kubectl describe --help`

#### GET SPECIFIC WHEN EXPLAINING/DESCRIBING OBJECTS:

`kubectl explain pod.spec`
 
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

## WORKING WITH HARBOR

#### PULL OR PUSH AN IMAGE FROM AN OCI IMAGE REGISTRY LIKE HARBOR OR DOCKERHB
`docker pull|push "${HARBOR_DOMAIN}/app-top-level_folder/app:tag"`

#### TAG AN IMAGE TO PUSH TO HARBOR 
`docker image tag "${HARBOR_DOMAIN/app-top-level-folder/app:current-tag" "${HARBOR_DOMAIN}/app-top-level-folder/app:new-tag"`

#### COPY ONE IMAGE FROM AN OCI REGISTRY TO ANOTHER OCI REGISTRY
`imgpkg copy -i "${HARBOR_DOMAIN}/app-top-level-folder/app@sha256:sha-string-goes-here" --to-repo "${HARBOR_DOMAIN}/app-top-level-folder/app"`

#### SECURITY AND NETWORKING (OBJECT NAME COULD BE svc, pr, etc)

`kubectl port-forward objectname/app-name 8080:8080`

#### GET NETWORK POLICY

kubectl get NetworkPolicy

#### LIST SECRETS

kubectl get secrets --all-namespaces

#### GENERATE A SECRET

echo -n 'password' | base64 -d

#### GET SECRET

`kubectl get secret cluster-kubeconfig`

#### GET SECRET FROM CONFIG FILE

`kubectl get secret cluster-kubeconfig -o jsonpath="{.data.value}"`

