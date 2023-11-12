# kube-monkey cheatsheet
kube monkey is an implementation of netflix chaos monkey and it's specially built for kubernetes clusters. So, kube-monkey periodically schedules a list of pod termination events and by terminating the pods it's very useful for us to test the fault tolerance of your highly available system and the pod termination is one of the chaos engineering experiment that run on kubernetes to make sure the replica set is working on and your application is not facing any downtime.

## contents
- how to install kube-monkey onto kubernetes
- enable kube-monkey in a demo mode and we will quickly see it in action
- install and label applications to make them eligible targets for chaos engineering experiment

### get version
```bash
kubectl version
```
```bash
kubectl version --short
```

### get component status
```bash
kubectl get componentstatus
```

### get nodes
```bash
kubectl get nodes
```
```bash
kubectl cluster-info
```

# package manager in kubernetes
Helm is the package manager used for installing applications onto kubernetes.

### get version
```bash
helm version --short
```

### create namespace
```bash
kubectl create namespace kube-monkey
```

### grab source code for helm chart
```bash
git clone https://github.com/asobti/kube-monkey && pushd kube-monkey/helm
```

### install helm chart
```bash
helm install my-monkey kubemonkey -n kube-monkey -f ~/my-monkey.yaml
```

### check status
```bash
kubectl -n kube-monkey rollout status deployment my-monkey-kube-monkey
```

### see logs
```bash
kubectl logs -f deployment.apps/my-monkey-kube-monkey -n kube-monkey
```
```bash
kubectl logs -f deployment.apps/<app-name> -n <namespace-name>
```

# demo purpose

### create nginx yaml file
```bash
kubectl apply -f nginx.yaml
```

### add more pods: create a namespace called more-apps
```bash
kubectl create namespace more-apps
```
```bash
kubectl apply --namespace more-apps -f ghost.yaml
```
kube-monkey enabled from nginx.yaml  
![image](https://github.com/hatmahat/kube-monkey/assets/56577748/d7a207e0-0e94-4cf7-a4bc-5aed8e623db5)

[reference](https://www.youtube.com/watch?v=ic4k-FkYU44&t=118s&ab_channel=TechnologyFirst)
