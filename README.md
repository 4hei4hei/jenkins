# jenkins
DockerでJenkinsを起動する

masterノードとslave2台をcomposeで起動する

# 雑セットアップ手順
masterノード起動後、ブラウザで管理画面を開く

プラグインはrecomendedを選択してインストール

masterノードでssh鍵生成
```
docker exec -it master ssh-keygen -t -C""
```
生成後、ホスト側のディレクトリからも鍵ファイルを参照できるため、公開鍵を確認

slaveノードの環境変数に公開鍵をペーストする

管理画面からslaveノードをAgentとして追加する

Agentに保持させる鍵情報に秘密鍵を利用する

Agentが追加される

# 参考
- 山田明憲, "Docker/Kubernetes 実践コンテナ開発入門", 技術評論社 (2018/8/25),ISBN-10:4297100339, ISBN-13:978-4297100339,
https://www.amazon.co.jp/dp/4297100339

- https://qiita.com/keropon1274/items/45c61a7efe218850aed7

- https://qiita.com/michi-michi/items/b1835d6e89856643b65a
