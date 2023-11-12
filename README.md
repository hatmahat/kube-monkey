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
