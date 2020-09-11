# Docker on Vagrant PHP7.3開発環境

Vagrant上でDockerを動かしPHP開発環境を構築するサンプル。

* PHP7.3
* Nginx
* MariaDB
* PostgreSQL
* Node.js


## 説明

### Vagrant
Dockerホスト用OS「barge」を使用。
docker-composeのインストール・起動を行う。

プライベートネットワークをDHCPで起動。
vagrant-hostmangerで、hostsの更新を行う。


#### Vagrantプラグイン

* vagrant-vbguest
* dotenv
* vagrant-disksize
* vagrant-hostsupdater
* vagrant-hostmanager

### Docker
docker-compose.ymlで設定。
`src`ディレクトリにプログラムを設置する。

## 使用例
```
vagrant up
```

```
vagrant ssh
```

```
docker-compose exec workspace bash
```

##### Laravelインストール
```
composer create-project --prefer-dist laravel/laravel=6.* .
```

##### 設定
`.env`
```ini
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=vagrant
DB_USERNAME=vagrant
DB_PASSWORD=vagrant
```

##### 確認

http://phpdev.test
