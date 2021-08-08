# jenkins
DockerでJenkinsを起動する

masterノードとslave2台をcomposeで起動する

# 雑セットアップ手順
最初に以下を実行

```
docker-compose up -d
```

masterノード起動後、ブラウザで管理画面を開く

プラグインは"install suggested plugin"を選択

masterノードでssh鍵生成
```
docker exec -it master ssh-keygen -t rsa -C""
```
生成後、ホスト側のディレクトリからも鍵ファイルを参照できるため、公開鍵を確認

slaveノードの環境変数に公開鍵をペーストする (※1)

※ var.env経由で変数に入れる場合は以下の手順でコンテナを再起動

```
docker-compose stop
docker-compose up -d
```

管理画面からslaveノードをAgentとして追加する

- 管理画面 >> jenkinsの管理 >> ノードの管理 >> 新規ノード作成

|  項目  |  内容  |
| ---- | ---- |
|  ノード名  |  slave0*  |
|  Parmanent Agent  |  チェック有  |
|  リモートFSディレクトリ  |  /home/jenkins  |
|  起動方法  |  SSH経由でUnixマシンのスレーブエージェントを起動 |
|  認証方法  |  追加 (後述)  |
|  Host Key Verification Strategy  |  Non verifying verifycation strategy  |
|  高度な設定 >> Javaのパス  |  /opt/java/openjdk/bin/java  |

- 認証方法の追加 ("任意"の箇所は作成時に設定したものを括弧内に例として記載)

| 項目 | 内容 |
| ---- | ---- |
| 種類 | sshユーザーと秘密鍵 |
| ID | 任意 (slave) |
| ユーザー名 | 任意 (jenkins) |
| 秘密鍵 | 直接入力 (秘密鍵をペースト (※1で作成したもの)) |

Agentが追加される

# 参考
- 山田明憲, "Docker/Kubernetes 実践コンテナ開発入門", 技術評論社 (2018/8/25),ISBN-10:4297100339, ISBN-13:978-4297100339,
https://www.amazon.co.jp/dp/4297100339

- https://qiita.com/keropon1274/items/45c61a7efe218850aed7

- https://qiita.com/michi-michi/items/b1835d6e89856643b65a

