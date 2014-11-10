# Vagrant+AnsiebleによるLAMP環境のサンプル

## 手順

1 

```sh
vagrant up
```
でVMを起動


2 

```sh
ansible lamp -m ping -i inventory_file -vvvv
```
が成功することを確認


3 

```sh
ansible lamp -m shell -a 'pwd; ls -la;' -i inventory_file -vvvv
```
を実行するとVM内でコマンドが実行できるていることが確認できる


4 

```sh
ansible-playbook -i inventory_file lamp.yml -vvv --ask-sudo-pass
sudo password:[自分のPCのrootパスワード]
```
を実行して

http://lamp.test/

にアクセスして

hello test lamp

というページが表示されることを確認する


4 

リポジトリにあるVagrantfile.newをVagrantファイルにしてから
```sh
vagrant destroy
default: Are you sure you want to destroy the 'default' VM? [y/N] y
```
で一旦VMを削除して、

```sh
vagrant up
~
sudo password:[自分のPCのrootパスワード]
```
ではじめのVM作成時にansibleを実行することができる

ここで実行しているコマンドは

```sh
vagrant provision
```
コマンドで再実行することもできる


### 注意点

新しく
```sh
vagrant up
```
したりansibleでプロビジョニングを行うと古い.ssh/known_host情報とssh情報が違うと言われてエラーになることがあるので、
その場合は  
~/.ssh/known_host  
内にある192.168.34.10のある行を削除してから行う


## バージョンなど
CentOS 6.5

https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box

PHP 5.5

[root@vagrant-centos65 ~]# php -v  
PHP 5.5.18 (cli) (built: Oct 16 2014 12:21:51)  
Copyright (c) 1997-2014 The PHP Group  
Zend Engine v2.5.0, Copyright (c) 1998-2014 Zend Technologies

apache 2.2

[root@vagrant-centos65 ~]# apachectl -v  
Server version: Apache/2.2.15 (Unix)  
Server built:   Oct 16 2014 14:48:21

MySQL 5.5

[root@vagrant-centos65 vagrant]# mysql  
Welcome to the MySQL monitor.  Commands end with ; or \g.  
Your MySQL connection id is 2  
Server version: 5.5.40 MySQL Community Server (GPL) by Remi

