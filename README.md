# BASIC COMPONENTS

## ETCD COMMANDS

#### VIEW ETCD OPTIONS

```bash
cat /etc/kubernetes/manifests/etcd.yaml
```

#### SET A KEY VALUE PAIR IN THE ETCD DATABASE

```shell
./etcdctl set key value
```

#### GET A KEY IN ETCD

```shell
./etcdctl get key
```

## KUBE-APISERVER

#### VIEW KUBE-APISERVER

```shell
kubectl get pods -n kube-system
```

#### VIEW KUBE-APISERVER OPTIONS

```shell
cat /etc/kubernetes/manifests/kube-apiserver.yaml
```

## KUBE-PROXY

```shell
kubectl get pods -n kube-system | grep kube-proxy
```

## KUBE-CONTROLLER-MANAGER

#### VIEW KUBE-CONTROLLER-MANAGER OPTIONS

`cat /etc/kubernetes/manifests/kube-controller-manager.yaml`

## KUBE-SCHEDULER


#### VIEW KUBE-SCHEDULER OPTIONS

```shell
cat /etc/kubernetes/manifests/kube-controller-manager.yaml
```

#### VIEW KUBE-SCHEDULER PROCESS

```shell
ps -aux | grep kube-scheudler
```

## KUBELET

#### SEE IF KUBELET IS RUNNING

```shell
ps -aux | grep kublet
```

#### SEE IF KUBELET IS RUNNING

```shell
ps -aux | grep kubelet
```

# CREATING MANIFESTS

## CREATE A DEPLOYMENT

`deployment.def.yaml`

```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp-deployment
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-frontend
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end
 ```

### RUN THE DEPLOYMENT

```shell
kubectl create -f deployment-def.yaml
```
#### VIEW THE DEPLOYMENT

```shell
kubectl get deployment | grep deployment-def
```
#### VIEW REPLICASET CREATED BY THE DEPLOYMENT

```shell
kubectl get replicaset | grep myapp
```
#### VIEW PODS CREATED DURING THE DEPLOYMENT

```shell
kubectl get pods | grep myapp
```

### USE THE -w FLAG TO WATCH RESOURCES GENERATE IN REAL-TIME

```shell
kubectl get pods -w
```

#### VIEW POD COUNT WITH NO HEADERS TO GET AN ACCURATE NUMBER

```shell
kubectl get pods --no-headers | wc -l
```

#### ALTERNATE METHOD

```shell
kubectl get pods | tail -n +2 | wc -l
```

#### SCALE UP OR DOWN YOUR DEPLOYMENT

```shell
kubectl scale --replicas=8 -f deployment-ref.yaml
```
### TO SEE THE WHOLE DEPLOYMENT AT ONCE

```shell
kubectl get all
```
### ADD A SERVICE TO EXPOSE THE APPLICATION

```
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
  spec:
    type: NodePort
    ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
    selector:
      app: myapp
      type: front-end
  ```
  ### APPLY THE SERVICE
  
  ```shell
  kube
 ### WITH EVEN MORE INFO

```shell
kubectl get all -A
```

### MAX INFO

```shell
kubectl get all -A -o wide
```

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

`kubectl get NetworkPolicy`

#### 19. LIST SECRETS

`kubectl get secrets --all-namespaces`

#### 20. GENERATE A SECRET

`echo -n 'password' | base64 -d`

#### 21. GET SECRET

`kubectl get secret cluster-kubeconfig`

#### 22. GET SECRET FROM CONFIG FILE

`kubectl get secret cluster-kubeconfig -o jsonpath="{.data.value}"`

#### 23. LIST AUTHENTICATED CONTEXTS

```shell
kubectl config get-contexts, ~/.kube/config
```

#### 24. SWITCH CONTEXT

```shell
kubectl config use-context
```

#### 25. DELETE CONTEXT

`kubectl config delete-context`

#### 26. LIST CERTIFICATES

`kubectl get csr`

#### 27. CHECK USER PRIVILEDGE

`kubectl auth can-i use pods/list`

## WORKING WITH TANZU & CARVEL

#### 1. PULL OR PUSH AN IMAGE FROM AN OCI IMAGE REGISTRY LIKE HARBOR OR DOCKERHB
`docker pull|push "${HARBOR_DOMAIN}/app-top-level_folder/app:tag"`

#### 2. TAG AN IMAGE TO PUSH TO HARBOR 
`docker image tag "${HARBOR_DOMAIN/app-top-level-folder/app:current-tag" "${HARBOR_DOMAIN}/app-top-level-folder/app:new-tag"`

#### 3. COPY ONE IMAGE FROM AN OCI REGISTRY TO ANOTHER OCI REGISTRY
`imgpkg copy -i "${HARBOR_DOMAIN}/app-top-level-folder/app@sha256:sha-string-goes-here" --to-repo "${HARBOR_DOMAIN}/app-top-level-folder/app"`

#### 4. USING KP SECRETS

`kp secret create "harbor-cred-${USER}" --registry "${HARBOR_DOMAIN}" --registry-user "${USER}"`

#### 5. CONNECT TBS AND HARBOR

`kp image create app --tag "${HARBOR_DOMAIN}/app-folder/app-name:app-tag" --git "https://github.com/${GH_USERNAME}/simple-app.git" --git-revision main --wait --namespace "${USER_ID}"`

#### 6. RELOCATE IMAGES USING TBS

`imgpkg copy -b registry.tanzu.vmware.com/build-service/bundle:1.4.2 --to-repo <IMAGE-REPOSITORY>`

### 7. PULL IMAGE FROM TANZU BUILD SERVICE
`docker pull registry.tanzu.vmware.com/build-service/package-repo:sha256-ba0f8da86e8f2f0fb6563ced284e5cf0df9a82523f854b8eede213d4ce72230b.imgpkg`
