### 続き

- 送信者の変更をマージ
```console
git merge 送信者/first_pull_request
```
- 動作確認、テストする
- プルリクエスト送信先のブランチへマージ
```console
git checkout ogawaso/master
```
```console
git merge pr1
```
- pushする
```console
git push
```
- プルリクエストがclosedになっているはず
