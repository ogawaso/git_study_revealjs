# プルリクエストの練習について
## 目的
- githubフローと呼ばれる開発フローを体験
- コンフリクトしたソースのマージ作業を体験
- pull と pull --rebaseの違いを知る

## やり方
- 3人グループを組む(余ったら2人で)
- Aさんが一番詳しい人でB,Cさんを決める
- 前回やったことは手順に書いてないです。

## 手順
- Aさんがgithub上にgit_pr_studyという名前でリポジトリを作る
 - sample.rbというrubyスクリプトがあって動かすと「hello world!」が表示される
- BさんがAさんのリポジトリをフォークする
 - githubの画面上でfolkボタンを押す
- Bさんがfolkしたリポジトリをローカルにcloneして取得(terminal）
```console
git clone git@github.com:アカウント名/git_pr_study.git
```
- Bさんがローカルブランチ(pull-request1)を作って少し改修をする
 - 「hello pull request1!」になるようにする
- Bさんがgithubにブランチをpushする
- BさんがAさんにプルリクエストを送る
 - githubの画面上でリモートブランチの画面に移動
 - create pullrequestボタンがあるので押す
- CさんがAさんのリポジトリをfolkする
- Cさんがfolkしたリポジトリをローカルにcloneする
- Cさんがローカルブランチ(pull-request2)を作って少し改修をする
 - 「hello pull request3!」になるようにする
- Cさんがgithubにブランチをpushする
- CさんがAさんにプルリクエストを送る
- AさんがBさんのプルリクエストを承認
 - github上でプルリクエスト一覧からボタンを押す
- ボタンを押した後だとAさんがCさんのプルリクエストを受け取れないことをgithub上で確認
- Aさんがプルリクエストのコメントにコンフリクトしているからrebaseというコメント書く
- CさんがAさんのmasterリポジトリから差分を取得
 - Aさんのリモートリポジトリ情報を追加(git remote add)
 ```console
 git remote add Aさん git@github.com:Aさん/git_pr_study.git
 git checkout master
 git pull --rebase Aさん maste
 ```
 - Cさんがプルリクエストしたブランチにmasterの反映
 ```console
 git checkout pull-request2
 git rebase master
 ```
 - ここでコンフリクトが起こる
 - 修正したら以下の作業で直る
 ```console
 git add sample.rb
 git rebase --continue
 ```
 - リモートにpushする(-fが必要)
 ```console
 git push origin master -f
 ```
 - Cさんがリモートブランチをpushする
- AさんがCさんのプルリクエストをローカルでマージする
 - Cさんのプルリクエスト対象のブランチを取得する
 ```console
 git remote add Cさん git@github.com:Cさん/git_pr_study.git
 git fetch Cさん
 git checkout -b pull-request2 Cさん/pull-request2
 ```
 - ruby sample.rbして結果が問題ないことを確認
 - masterにマージ
 ```console
 git merge pull-request2
 ```
 - リモートにpush
 ```console
 git push origin master
 ```
- BさんもAさんから改修分を取得する
