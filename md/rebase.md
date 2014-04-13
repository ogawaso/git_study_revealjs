### マージできないとき
- プルリクエストを出した後、masterが更新されて編集した部分が衝突したら？
- プルリクエストで出したコミットたちを一旦masterとrebaseする必要がある
```console
git checkout master
```
- リモート上の最新を取得
```console
git pull  -rebase
```
