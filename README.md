Kubernetes Pod Creation and Management
1. Create Pod
Apply YAML Configuration
bash
Copy code
kubectl apply -f nginx-pod.yaml
Output:

bash
Copy code
pod/nginx-pod1 created
2. Pod Status and Information
List Pods
bash
Copy code
kubectl get pods
Output:

sql
Copy code
NAME         READY   STATUS    RESTARTS   AGE
nginx-pod    1/1     Running   0          123m
nginx-pod1   1/1     Running   0          9s
List Pods by Label
bash
Copy code
kubectl get pods -l app=todo
Output:

sql
Copy code
NAME         READY   STATUS    RESTARTS   AGE
nginx-pod1   1/1     Running   0          64s
Get Detailed Information of a Pod
bash
Copy code
kubectl get pod nginx-pod1 -o wide
Output:

sql
Copy code
NAME         READY   STATUS    RESTARTS   AGE    IP           NODE                NOMINATED NODE   READINESS GATES
nginx-pod1   1/1     Running   0          101s   10.244.1.5   local-cluster-m02   <none>           <none>
Describe a Pod
bash
Copy code
kubectl describe pod nginx-pod1
3. Port Forwarding
Forward Pod Port to Local Port
bash
Copy code
kubectl port-forward nginx-pod1 8083:80
Output:

csharp
Copy code
Forwarding from 127.0.0.1:8083 -> 80
Forwarding from [::1]:8083 -> 80
Handling connection for 8083
