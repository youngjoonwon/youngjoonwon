### Environment setup 

#### a. Windows/Mac/Linux

install docker desktop (download and install)

- https://docs.docker.com/desktop/install/mac-install/
- start docker desktop: this is to create, run, edit, and manage container images

#### b. minikube

create a (kubernetes) cluster on local machine

1. Install minikube for your OS (Step 1 from https://minikube.sigs.k8s.io/docs/start/)

   for example, using mac homebrew:

   ```
   $ brew install minikube
   $ zsh
   ```

2. install kubectl for your OS (https://kubernetes.io/docs/tasks/tools/)

   for example, using mac homebrew:

   ```
   $ brew install kubernetes-cli
   ```

3. start minikube

   ```
   $ minikube start
   ```

   e.g.)

   ```
   young-ultra] minikube start
   😄  minikube v1.33.1 on Darwin 14.5 (arm64)
   ✨  Automatically selected the docker driver
   📌  Using Docker Desktop driver with root privileges
   👍  Starting "minikube" primary control-plane node in "minikube" cluster
   🚜  Pulling base image v0.0.44 ...
   💾  Downloading Kubernetes v1.30.0 preload ...
       > preloaded-images-k8s-v18-v1...:  319.81 MiB / 319.81 MiB  100.00% 18.04 M
       > gcr.io/k8s-minikube/kicbase...:  435.76 MiB / 435.76 MiB  100.00% 21.47 M
   🔥  Creating docker container (CPUs=2, Memory=7789MB) ...
   🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
       ▪ Generating certificates and keys ...
       ▪ Booting up control plane ...
       ▪ Configuring RBAC rules ...
   🔗  Configuring bridge CNI (Container Networking Interface) ...
   🔎  Verifying Kubernetes components...
       ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
   🌟  Enabled addons: storage-provisioner, default-storageclass
   🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
   ```

4. create a cluster

   ```
   $ minikube kubectl -- get po -A
   $ minikube dashboard
   ```

   add the following to shell config (e.g., ~/.zshrc)

   ```shell
   alias kubectl="minikube kubectl --"
   ```

5. create a deployment and accessible on port 8080 (on local machine)

   ```shell
   $ kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   $ kubectl expose deployment hello-minikube --type=NodePort --port=8080
   ```

   ```shell
   $ kubectl get services hello-minikube
   ```

   ```shell
   $ kubectl port-forward service/hello-minikube 7080:8080
   ```

   open a browser and goto http://localhost:7080/

6. pause/halt/delete cluster

   ```shell
   $ minikube pause
   $ minikube stop
   $ minikube delete --all
   ```

   











