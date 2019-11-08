# concourse-example

[Concourse](https://concourse-ci.org/)の例です。

[Docker](https://www.docker.com/)を利用してローカルホストで試せるようにしています。

## 必要なもの

- [Git](https://git-scm.com/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 準備

まずは準備が必要です。

1. このリポジトリをcloneする
2. コンテナを起動
3. Nexusのパスワードを変更する
4. GitBucketへリポジトリをpushする

### 1. このリポジトリをcloneする

任意の場所へcloneしてください。

```sh
git clone https://github.com/backpaper0/concourse-example.git
```

### 2. コンテナを起動

Docker Composeでコンテナを起動してください。

```sh
cd concourse-example
docker-compose up -d
```

起動するアプリケーションは次の通りです。
なおNexusは起動に少し時間がかかります。

|名前|URL|ユーザー名|パスワード|
|---|---|---|---|
|Concourse|http://localhost:8080/|`demo`|`demo`|
|Nexus|http://localhost:8081/|`admin`|※後述|
|GitBucket|http://localhost:8000/|`root`|`root`|

Nexusのパスワードはコンテナ内の`/nexus-data/amdin.password`に記載されています。

### 3. Nexusのパスワードを変更する

Nexusへサインインしてください。
アカウントは`admin`です。
初期パスワードは次のコマンドで確認できます。

```sh
docker-compose exec nexus cat /nexus-data/admin.password
```

初回サインイン時にパスワードの変更が求められるので`admin`にしてください。

Anonymous Accessはチェックを入れて有効化しておいてください。

### 4. GitBucketへリポジトリをpushする

GitBucketへ`root`でログインして`demo`という名前の空のリポジトリを作成してください。

空のリポジトリに内容を`push`します。

```sh
git clone https://github.com/backpaper0/demo.git
cd demo
git remote add demo http://localhost:8000/git/root/demo.git
git push demo master
```

## WIP パイプラインを登録してビルドする

### flyコマンドのインストール

### ログイン

```sh
fly -t main login -c http://localhost:8080
```

### パイプラインを登録する

```
fly -t main sp -p demo -c pipelines/demo.yml
fly -t main up -p demo
```

