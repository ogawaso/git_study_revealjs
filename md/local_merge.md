### 受け取ったプルリクエストを手動で反映
- 画面上だけの確認だと動作確認できない
- そういうときはローカルPC上にプルリクエストされたブランチを取得して動作確認
```console
git remote add 送信者 git@github.com:送信者/git_pr_study.git
```
- リポジトリ情報を取得
```console
git fetch 送信者
```

- 動作確認用のbranchを作成
```console
git checkout -b pr1
```
