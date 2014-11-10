# 手順

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

