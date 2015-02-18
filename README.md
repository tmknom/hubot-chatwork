# ChatWork × Hubot 連携スクリプト


## 事前準備

事前に、Hubot用のユーザをChatWorkに作成しておき、APIのアクセストークンを発行しておく。

申請方法は、公式ドキュメントを参考に。
http://developer.chatwork.com/ja/index.html


## ローカルで動かす

### 前提条件

* node.jsがインストール済みであること
* Hubotがインストール済みであること

### セットアップ

```bash
$ git clone git@github.com:tmknom/hubot-chatwork.git
$ cd hubot-chatwork
$ npm install
```

### 環境変数のセット

```bash
$ export HUBOT_CHATWORK_TOKEN="xxxxxxxx"
$ export HUBOT_CHATWORK_ROOMS="12345678"
$ export HUBOT_CHATWORK_API_RATE="600"
```

### Hubotの起動

```bash
$ bin/hubot -a chatwork
```

### 動作確認

先ほど環境変数でセットした、ChatWorkのグループチャット上で、「hubot ping」と入力。

HubotユーザがChatWork上で「PONG」と応答すればOK。


## Herokuへデプロイ

### 前提条件

* Herokuのアカウントが作成済みであるとと
* Heroku Toolbeltがインストール済みであること

### Herokuへアプリケーションをpush

```bash
$ heroku login
$ heroku create
$ git push heroku master
```

### HerokuへChatWork連携用の情報を登録

```bash
$ heroku config:add HUBOT_CHATWORK_TOKEN="xxxxxx"
$ heroku config:add HUBOT_CHATWORK_ROOMS="1234"
$ heroku config:add HUBOT_CHATWORK_API_RATE="600" 
```

### Herokuのアイドリング防止設定

```bash
heroku config:set HUBOT_HEROKU_KEEPALIVE_URL=$(heroku apps:info -s | grep web_url | cut -d= -f2)
```

### Herokuのタイムゾーン変更

```bash
$ heroku config:add TZ=Asia/Tokyo
```

### 動作確認

ローカルの時と同様。

