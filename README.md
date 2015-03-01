概要
----

CakePHPの実行に最適化したLAMP環境のVagrantfileです。インストールされるソフトウェアは主に下記になります。詳しくは/vagrant/Vagrantfileを参照して下さい。

* CentOS
* Apache
* PHP
* MySQL
* phpMyAdmin

前提
----

* VirtualBoxおよびVagrantをインストール済である事

使い方
----

はじめにこのGitリポジトリをCloneします。

```
$ git clone https://github.com/relationslab/vagrant-lamp-cakephp
```

次にMySQLの設定を行います。/vagrant/scriptsに作成するユーザーとDBの情報を指定します。もしMySQL生成時にDDLを流したい場合はddl.sqlにDDLを記述してください。

準備が整ったらvagantフォルダに移動しvagrant upしてください。するとLAMP環境が生成されます。

```
$ cd vagrant
$ vagrant up
```

環境が生成されるまでにしばらくかかります。環境が生成されたらSSHで接続します。

```
$ vagrant ssh
```

次にCakePHPのアプリケーションのGitリポジトリを/share/配下にCloneしてください。

これで下記のURLをホストOSのブラウザで確認するとアプリケーションの画面が確認できると思います。phpMyAdminもインストール済になっています。

```
http://192.168.33.40/
http://192.168.33.40/phpMyAdmin/
```

次にこのGitリポジトリからAWSの環境にデプロイができるようにAWSDevToolsをセットアップします。

```
$ pwd
/share/CiD_Beta
$ sh ~/.aws/AWS-ElasticBeanstalk-CLI-2.5.1/AWSDevTools/Linux/AWSDevTools-RepositorySetup.sh 
```

下記のコマンドで、AWSの資格情報と環境情報を設定します。

```
$ git aws.config
```


