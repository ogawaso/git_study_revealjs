## reflog
- コマンド操作の作業の歴史を閲覧できる
```console
git reflog
```
- 過去の状態に戻すことができる
- 指定した作業の復元ではない
- 間違ってgit reset  --hardしてコミット消したときとか便利
```console
git reset --hard HEAD@{1}
```
