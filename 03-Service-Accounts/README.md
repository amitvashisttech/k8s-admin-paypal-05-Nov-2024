
Documentation Referred:

https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/

#### Authenticating with Token:
```sh
kubectl create sa custom-sa
kubectl apply -f pod-1.yaml
kubectl exec -it pod-1 -- bash
```
```sh
TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)
echo $TOKEN
curl -k -H "Authorization: Bearer $TOKEN" "https://kubernetes/api/v1"
curl -k -H "Authorization: Bearer $TOKEN" "https://kubernetes/api/v1/namespaces"
```

### Approach 1 - Opt out AutoMounting at Service Account level (Reference):

Following is a demo snippet for reference. We have not used this in our practicals.
```sh
apiVersion: v1
kind: ServiceAccount
metadata:
  name: custom-sa
automountServiceAccountToken: false
```

For our practical, we had added the automountServiceAccountToken in default service account
```sh
kubectl edit sa default
```
Add following snippet:

automountServiceAccountToken: false

To verify if this approach is working, let's perform some tests.
```sh
kubectl run pod-2 --image=nginx
kubectl exec -it pod-2 -- bash
cd /run
ls
```
Once tested, you can undo the change so that we can experiment with Approach 2.

### Approach 2 Opt out AutoMounting at POD level

#### Create POD with AutoMounting Disabled:

```sh
nano pod-3.yaml
```
```sh
apiVersion: v1
kind: Pod
metadata:
  name: pod-3
spec:
  automountServiceAccountToken: false
  containers:
  - image: nginx
    name: pod-3
```
```sh
kubectl apply -f pod-3.yaml
```

### Verification Stage:

```sh
kubectl exec -it pod-3 -- bash
cd /run
ls
```



### Now Grant Cluster-Admin Role to custom-sa service account 
```
kubectl create clusterrolebinding admin-rolebindngs --clusterrole=cluster-admin --serviceaccount=default:custom-sa
```


```sh
TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)
echo $TOKEN
curl -k -H "Authorization: Bearer $TOKEN" "https://kubernetes/api/v1"
curl -k -H "Authorization: Bearer $TOKEN" "https://kubernetes/api/v1/namespaces"
```

Note: In case you are getting lookup error then replace kuberntes with service IP : 10.96.0.1 "kubectl  get svc"  

