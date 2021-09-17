### Intro

For testing and interacting with your dialogue applications you will use a remote Kubernetes cluster which is running in "eduserv". You will develop your DDDs in your local machine and sync your local files with your namespace in the remote cluster.

This document will guide you on your way to set up your access to the Kubernetes cluster running in eduserv.


### Requirements

They are already installed in eduserv and (maybe) in the lab computers, but in case you want to work in your own computer we leave them here. All of them are console-based and we can confirm that they work in Linux and Mac (Unix) consoles for sure.

This includes "windows subsystem for linux" (WSL) consoles in Windows 10 (as they are in fact Linux consoles running inside your Windows 10). If you are using Windows 10 and do not have WSL, check how to install it here: https://docs.microsoft.com/en-us/windows/wsl/install-win10

- Tala SDK (`pip install tala`). NOTE: The newest Tala versions support Python 3.9! We cannot assure they will work well with older version of Python.
- Okteto CLI (https://okteto.com/docs/getting-started/installation)
- Kubectl (https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- ONLY for MacOS users: libmagic (`brew install libmagic`).


### Setting up access to the remote Kubernetes cluster

You may need to follow steps 1-4 only once for setting this up.

1. Log into to "eduserv" via SSH. In order to access the Kubernetes cluster from your machine, you need to tunnel the port 16443 to your localhost (aka 127.0.0.1).
`ssh -p 62266 -Y -L 16443:127.0.0.1:16443 gusXXXXXX@eduserv.flov.gu.se`
You just need to start this session and let it run on the background. Run the rest of the steps in your own machine as the requirements specified above are not installed in the eduserv.

2. Download the "config" file, which you can find in the Lab 2 instructions and in the "Files" section in Canvas.

3. Installing "kubectl" doesn't create the kube config file a lot of times ("~/.kube/config). If you don't have it, you can create it manually by running:
  - `mkdir ~/.kube` (~ is your user directory)
  - Put the "config" file inside the ".kube" folder that you just created.

4. In Kubectl, you have to select the "microk8s-eduserv" context to connect it to the Kubernetes cluster.
`kubectl config use-context microk8s-eduserv`

5. Each of you has a namespace in the Kubernetes cluster (the namespace name is your "gus..." username). Such namespace contains all the different components necessary to run your dialogue applications in it. To access your namespace:
`kubectl config set-context microk8s-eduserv --namespace=gusXXXXXX`

