# Kubernetes-Jupyternote
Значком "$" помечены команды в терминале 

#Установка
#Установить apt-репозиторий Kubernetes.

$ apt-get update && apt-get install -y apt-transport-https
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
$ cat </etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main  

#Установить kubelet, kubeadm и kubernetes-cni.
$ apt-get update
$ apt-get install -y kubelet kubeadm kubernetes-cni

#Установить helm

#скачать-> https://github.com/helm/helm/releases

$ tar -zxvf helm-v2.0.0-linux-amd64.tgz
$ mv linux-amd64/helm /usr/local/bin/helm

#Вход под суперпользователем
$sudo -i

$swapoff -a #kubeadm имеет некоторые напряженности со swap

$kubeadm init #инициализация кластера

#настройка переменных окружения
$ cd $HOME
$ sudo whoami
$ sudo cp /etc/kubernetes/admin.conf $HOME/
$ sudo chown $(id -u):$(id -g) $HOME/admin.conf
$ export KUBECONFIG=$HOME/admin.conf
$ echo "export KUBECONFIG=$HOME/admin.conf" | tee -a ~/.bashrc

kubectl create -f https://raw.githubusercontent.com/kubernetes-incubator/client-python/master/examples/notebooks/docker/jupyter.yml
