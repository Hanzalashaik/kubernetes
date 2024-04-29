# kubernetes

hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl apply -f nginx-pod.yaml
pod/nginx-pod1 created

hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl get po
NAME         READY   STATUS    RESTARTS   AGE
nginx-pod    1/1     Running   0          123m
nginx-pod1   1/1     Running   0          9s

hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl get pods -l app=todo
NAME         READY   STATUS    RESTARTS   AGE
nginx-pod1   1/1     Running   0          64s

hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl get pod nginx-pod1 -o wide
NAME         READY   STATUS    RESTARTS   AGE    IP           NODE                NOMINATED NODE   READINESS GATES
nginx-pod1   1/1     Running   0          101s   10.244.1.5   local-cluster-m02   <none>           <none>

hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl get pod nginx-pod1 -o yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"todo","team":"integerations"},"name":"nginx-pod1","namespace":"default"},"spec":{"containers":[{"image":"nginx:latest","name":"nginx-container","ports":[{"containerPort":80}]}]}}
  creationTimestamp: "2024-04-29T13:01:43Z"
  labels:
    app: todo
    team: integerations
  name: nginx-pod1
  namespace: default
  resourceVersion: "10208"
  uid: ec3eab41-f30e-43eb-9c23-80d53263e0c6
spec:
  containers:
  - image: nginx:latest
    imagePullPolicy: Always
    name: nginx-container
    ports:
    - containerPort: 80
      protocol: TCP
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-zwjdr
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: local-cluster-m02
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-zwjdr
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2024-04-29T13:01:43Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2024-04-29T13:01:50Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2024-04-29T13:01:50Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2024-04-29T13:01:43Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://5bbff09a3b910202f94ec904473b000119c4a497050ce8d06e739f4ca1d13779
    image: nginx:latest
    imageID: docker-pullable://nginx@sha256:ed6d2c43c8fbcd3eaa44c9dab6d94cb346234476230dc1681227aa72d07181ee
    lastState: {}
    name: nginx-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-04-29T13:01:49Z"
  hostIP: 192.168.58.3
  phase: Running
  podIP: 10.244.1.5
  podIPs:
  - ip: 10.244.1.5
  qosClass: BestEffort
  startTime: "2024-04-29T13:01:43Z"
hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl describe nginx-pod1
error: the server doesn't have a resource type "nginx-pod1"
hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl describe pod  nginx-pod1
Name:             nginx-pod1
Namespace:        default
Priority:         0
Service Account:  default
Node:             local-cluster-m02/192.168.58.3
Start Time:       Mon, 29 Apr 2024 18:31:43 +0530
Labels:           app=todo
                  team=integerations
Annotations:      <none>
Status:           Running
IP:               10.244.1.5
IPs:
  IP:  10.244.1.5
Containers:
  nginx-container:
    Container ID:   docker://5bbff09a3b910202f94ec904473b000119c4a497050ce8d06e739f4ca1d13779
    Image:          nginx:latest
    Image ID:       docker-pullable://nginx@sha256:ed6d2c43c8fbcd3eaa44c9dab6d94cb346234476230dc1681227aa72d07181ee
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Mon, 29 Apr 2024 18:31:49 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zwjdr (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-zwjdr:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m31s  default-scheduler  Successfully assigned default/nginx-pod1 to local-cluster-m02
  Normal  Pulling    2m30s  kubelet            Pulling image "nginx:latest"
  Normal  Pulled     2m25s  kubelet            Successfully pulled image "nginx:latest" in 5.573s (5.573s including waiting)
  Normal  Created    2m25s  kubelet            Created container nginx-container
  Normal  Started    2m25s  kubelet            Started container nginx-container

hanzala@hanzala:~/Desktop/github/kubernetes$ kubectl port-forward nginx-pod1 8083:80
Forwarding from 127.0.0.1:8083 -> 80
Forwarding from [::1]:8083 -> 80
Handling connection for 8083
