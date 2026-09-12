# Setup ArgoCD to pull from a Repository

#### 1. Create a repository on GitHub or Gitlab
[Kubernetes Resources](https://github.com/ManthanDhole/kubernetes-resources)

#### 2. Create a SSH Key and get the private & public keys

```
ssh-keygen

Give Custom Name for the KeyGen File: 
~/.ssh/id_ed25519_argo
```

#### 3. Add the ssh key to GitHub to allow access to ArgoCD 

```
cat ~/.ssh/id_ed25519_argo.pub

GitHub Settings > SSH and GPG Keys > New SSH Key > Title > Enter Public Key
```

#### 4. Configure Argo to pull from the GitHub Repository

```
cat ~/.ssh/id_ed25519_argo

Argo Settings > Repositories > Connect Repo > Connection Method (SSH) > 
Enter Name > Project (Default) >
Repository URL (git@github.com:ManthanDhole/kubernetes-resources.git) > 
SSH Private Key Data > Connect
```
Confirm if the connection has been marked as SUCCESSFUL or not.