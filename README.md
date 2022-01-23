# kubernetes-cheat-sheet
## KUBERNETES (AND MORE) COMMAND CHEAT SHEET

#### 1. SETTING QUESTION CONTEXT IN CKA EXAM:
`kubectl config set-context <context-of-question> --namespace=<namespace-of-question>`

#### 2. SET ALIAS FOR KUBECTL:
`alias k=kubectl`

#### 3. FIND SHORTNAMES FOR RESOURCES:
`kubectl api-resources`

#### 4. IMMEDIATELY DELETE A RESOURCE:
`kubectl delete pod nginx --grace-period=0 --force`

#### 5. FINDING OBJECT INFORMATION:
`kubectl describe pods | grep -C 10 "item to look for"`

#### OR IN YAML FORMAT:
`kubectl get pods -o yaml | grep -C 5 labels:`

#### 6. USING HELP FOR COMMANDS:
`kubectl delete --help`
`kubectl create --help`
`kubectl describe --help`

#### 7. GET SPECIFIC WHEN EXPLAINING/DESCRIBING OBJECTS:

`kubectl explain pod.spec`
 
#### 8. KUBERNETES AUTO-COMPLETION
`echo 'source <(kubectl completion bash)' >>~/.bashrc`

#### 9. GET CLUSTERS
`kubectl get clusters`

#### 10. GET NODES
`kubectl get nodes`

#### 11. GET NAMESPACE
`kubectl get namespaces`

#### 12. GET PODS IN A NAMESPACE
`kubectl get pods -n <namespace>`

#### 13. CREATE A NAMESPACE
`kubectl create ns my-namespace`

#### 14. DESCRIBE PODS IN A NAMESPACE
`kubectl describe pods <podname> -n <namespace>`

#### 15. SWITCH CONTEXT TO A SPECIFIC NAMESPACE
`kubectl config set-context --current --namespace=my-namespace`

#### 16. GET PODS BY LABELS AND SELECTORS (-l IS SHORT FOR SELECTOR)
`kubectl get pods -l app=name-of-app -A`

#### 17.SECURITY AND NETWORKING (OBJECT NAME COULD BE svc, pr, etc)

`kubectl port-forward objectname/app-name 8080:8080`

#### 18. GET NETWORK POLICY

kubectl get NetworkPolicy

#### 19. LIST SECRETS

kubectl get secrets --all-namespaces

#### 20. GENERATE A SECRET

echo -n 'password' | base64 -d

#### 21. GET SECRET

`kubectl get secret cluster-kubeconfig`

#### 22. GET SECRET FROM CONFIG FILE

`kubectl get secret cluster-kubeconfig -o jsonpath="{.data.value}"`

#### 23. LIST AUTHENTICATED CONTEXTS

`kubectl config get-contexts, ~/.kube/config`

#### 24. SWITCH CONTEXT

`kubectl config use-context`

#### 25. DELETE CONTEXT

`kubectl config delete-context`

#### 26. LIST CERTIFICATES

`kubectl get csr`

#### 27. CHECK USER PRIVILEDGE

`kubectl auth can-i use pods/list`

## WORKING WITH HARBOR

#### PULL OR PUSH AN IMAGE FROM AN OCI IMAGE REGISTRY LIKE HARBOR OR DOCKERHB
`docker pull|push "${HARBOR_DOMAIN}/app-top-level_folder/app:tag"`

#### TAG AN IMAGE TO PUSH TO HARBOR 
`docker image tag "${HARBOR_DOMAIN/app-top-level-folder/app:current-tag" "${HARBOR_DOMAIN}/app-top-level-folder/app:new-tag"`

#### COPY ONE IMAGE FROM AN OCI REGISTRY TO ANOTHER OCI REGISTRY
`imgpkg copy -i "${HARBOR_DOMAIN}/app-top-level-folder/app@sha256:sha-string-goes-here" --to-repo "${HARBOR_DOMAIN}/app-top-level-folder/app"`

