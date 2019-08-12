## PVC Sample
> storageClassName에 본 폴더에 있는 storageclass를 자유로이 사용해주세요.

### YAML

``` yaml
apiVersion: v1  
kind: PersistentVolumeClaim  
metadata:  
  name: azure-managed-disk  
spec:  
  accessModes:  
  - ReadWriteOnce  
  storageClassName: managed-premium  
  resources:  
    requests:  
      storage: 5Gi  
```


## PVC Roles Sample
> PV binding을 위해 Cluster Role을 작성합니다.

### YAML
``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: system:azure-cloud-provider
rules:
- apiGroups: ['']
  resources: ['secrets']
  verbs:     ['get','create']
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: system:azure-cloud-provider
roleRef:
  kind: ClusterRole
  apiGroup: rbac.authorization.k8s.io
  name: system:azure-cloud-provider
subjects:
- kind: ServiceAccount
  name: persistent-volume-binder
  namespace: kube-system
```
