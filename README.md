概要
----

CakePHP+MySQLのVagrantfileです。インストールされるソフトウェアは主に下記になります。詳しくは/vagrant/Vagrantfileと/vagrant/script.shを参照して下さい。

* CentOS
* Apache
* PHP
* MySQL
* phpMyAdmin

前提
----

* Gitをインストール済である事
* VirtualBoxおよびVagrantをインストール済である事

はじめに
----

リポジトリの内容は下記のようになっています。

```
vagrant-cakephp-mysql/
　├ README.md
　└ vagrant/
　   ├ Vagrantfile
　 　├ script.sh
　 　├ httpd.conf
　 　└ etc
```

vagrant upすると、ゲストOSの/shareにホストOSのvagrant-cakephp-mysqlフォルダがマウントされます。Apacheで/share以下の任意のフォルダを公開する設定になっているので、vagrant-cakephp-mysql配下にアプリケーションのソースを配置して開発する事ができます。ホストOS（Mac・Windows）からお好みのテキストエディタとGitクライアントで開発を行ってください。

Apacheの設定はhttpd.confの下記の設定を修正する事で変更できます。

```
<VirtualHost *:80>
    DocumentRoot /share/CiD_Beta
</VirtualHost>
```

手順
----

はじめにこのGitリポジトリをcloneします。

```
$ git clone https://github.com/relationslab/vagrant-cakephp-mysql
```

次にMySQLの設定を行います。/vagrant/script.shに作成するユーザーとDBの情報を指定します。もしMySQL生成時にDDLを流したい場合はddl.sqlにDDLを記述してください。

準備が整ったらvagantフォルダに移動しvagrant upしてください。すると環境が生成されます。

```
$ cd vagrant
$ vagrant up
```

環境が生成されるまでにしばらくかかります。環境が生成されたらSSHで接続します。

```
$ vagrant ssh
```

次にCakePHPのアプリケーションのGitリポジトリを/share/配下にcloneしてください。

ホストOSからは下記のURLでブラウザからアプリケーションの動作を確認することができます。phpMyAdminもインストール済になっています。

```
http://192.168.33.40/
http://192.168.33.40/phpMyAdmin/
```

次にこのGitリポジトリからAWSの環境にデプロイができるようにAWSDevToolsをセットアップします。

```
$ pwd
/share/<アプリケーションのGitリポジトリ>
$ sh ~/.aws/AWS-ElasticBeanstalk-CLI-2.5.1/AWSDevTools/Linux/AWSDevTools-RepositorySetup.sh 
```

下記のコマンドで、AWS Elastic Beanstalkの資格情報と環境情報を設定します。

```
$ git aws.config
```

aws.configで設定を行ったら、下記のコマンドでAWS Elastic Beanstalkの環境にアプリケーションをデプロイする事ができます。

```
$ git aws.push [--environment <environment_name>]
```

Vagrantの環境を停止する場合はホストOSの環境で/vagrantフォルダに移動し下記のコマンドを実行します。

```
$ vagrant halt
```

