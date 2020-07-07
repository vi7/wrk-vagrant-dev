Vagrant based local dev env
---------------------------

## Provision

### TODO

**repos**

k8s
```sh
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

docker ce
```sh
yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo
```

**packages and utils**

- helm (https://github.com/helm/helm/releases)

command:
```sh
yum -y install epel-release
yum -y install https://repo.ius.io/ius-release-el7.rpm
yum -y install yum-utils vim-enhanced tmux2u git222 python36 python36-pip bind-utils dig unzip traceroute
yum -y install docker-ce docker-ce-cli containerd.io
yum -y install kubectl
pip install ansible==2.8.2
```

**configs**

take those from helper-tools:
- .bashrc
- .bash_profile
- .vimrc
- .tmux.conf
- .gitconfig

git completion and prompt for bashrc

replace Git ver with the proper one

```sh
curl -L https://raw.githubusercontent.com/git/git/v2.22.3/contrib/completion/git-prompt.sh -o ~/.git-prompt.sh
```

kubectl and helm completion for bashrc

```sh
kubectl completion bash >/etc/bash_completion.d/kubectl
helm completion bash > /etc/bash_completion.d/helm
```

**services**

docker
```sh
systemctl enable docker
systemctl start docker
```

**puppet project**

TODO: for p39
