####コミットを消す(reset)
- インデックスに戻す
- HEADがコミットの一番最新地点
```console
git reset --soft HEAD~1
```

- ファイルの変更自体も消す
- (ワーキングディレクトリまで戻る)
```console
git reset --hard HEAD~1
```
