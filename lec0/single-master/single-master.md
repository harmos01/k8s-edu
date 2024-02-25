# 1.  git clone k8s-edu
```bash
## master-1에서 실행
## root로 실행
sudo su -
git clone https://github.com/io203/k8s-edu.git
cd k8s-edu/lec0/single-master
```

# 2. single-master rke2

## 2.1 master 설치
```bash

## root로 실행  
export EXTERNAL_IP=3.34.200.186
sh rke2-single-master-install.sh

source ~/.bashrc

watch kubectl get pod -A
## 9분정도 소요

## ubuntu유저 kubeconfig 설정
## ubuntu유저로 전환후 실행
exit

git clone https://github.com/io203/k8s-edu.git
cd k8s-edu/lec0/single-master

sh master-ubuntu-user-kubeconfig.sh
source ~/.bashrc

## debug
## journalctl -u rke2-server -f
```

## 2.2 master token  

master vm에서 실행  
```sh
sudo cat /var/lib/rancher/rke2/server/node-token

K107062ae12965fc4af5befb19c32b5ff6194dd9997e050d4951111e053d9b78454::server:ffe9e321b5509597d606a485c46b9e59

```

## 2.3 agent 설치
```sh
## worker-1/worker-2 실행 
## root로  설치 한다 
sudo su -
git clone https://github.com/io203/k8s-edu.git
cd k8s-edu/lec0/single-master

## master의 private IP를 입력 해야 함 
export MASTER01_INTERNAL_IP=172.26.0.42
export TOKEN=K107062ae12965fc4af5befb19c32b5ff6194dd9997e050d4951111e053d9b78454::server:ffe9e321b5509597d606a485c46b9e59
sh rke2-single-agent-install.sh

```

