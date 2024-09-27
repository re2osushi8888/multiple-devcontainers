# multiple-devcontainers
このリポジトリはdevcontainerを使ってフロントエンドアプリとバックエンドアプリを効率よく開発できることを目指すリポジトリです。

# 準備
## devcontainerのinstall
参考資料：https://blog.kinto-technologies.com/posts/2022-12-10-VSCodeDevContainer/

## gitの設定
ホスト側のgit情報をもとにdevcontainer内でgitを使う設定
### ユーザー情報を設定
```
$ git config --global user.name xxxx
$ git config --global user.email xxxx@xxxx.com
```
### sshキーの設定
※sshの公開鍵認証でgitの認証情報を使用する場合に行う

参考資料：https://qiita.com/shizuma/items/2b2f873a0034839e47ce

パスフレーズのない公開鍵を作成すること。パスフレーズがあるとdevcontainerがgitの情報を取得できない。


### ssh-agnetの設定
devcontainerはgitを使用する際、ホストPCのsshエージェントを取得し公開鍵の情報を取得する。
起動した時にssh-agentに公開鍵を登録する設定をする
```
# 起動時にssh-agentに公開鍵を登録する設定
$ echo 'eval "$(ssh-agent -s)" > dev/null 2>&1' >> ~/.bashrc
$ echo 'ssh-add ~/.ssh/{秘密鍵} > dev/null 2>&1' >> ~/.bashrc

# 設定を反映
$ source ~/.bashrc
```

# 動作確認
## ホスト側
### gitの公開鍵認証ができているか
```
$ ssh -T git@github.com
```
### devcontainerの起動
1. vscode上で「ctrl + shift + P」を入力
2. 「Dev Containers: Open Folder in Container」を選択
3. プロジェクトのルート（multiple-devcontainers）を選択
4. 開発用途に応じたdevcontainerを選択

## devcontainer側
### vscodeの確認
追加で入れた拡張機能やディレクトリ構成があっていることを確認する。
### gitの確認
下記のコマンドでホスト側で行った確認と同じ出力が出ることを確認。
```
$ ssh -T git@github.com
```

# 参考資料
- [Sharing Git credentials with your container]()
- [Known limitations
Dev Containers limitation](https://code.visualstudio.com/docs/devcontainers/containers#_known-limitations)
