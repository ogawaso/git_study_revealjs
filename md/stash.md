#### 編集の一時保存
- 少し編集
```console
echo 'puts "stash!"' >> sample.rb
```
- コミットするまではない編集を一時保存
```console
git stash
```
- 一時保存した修正一覧
```console
git stash list 
```

- 一時保存したものを取得
```console
git stash pop
```


