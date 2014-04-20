### マージする
- 差分が分かるようにちょっと修正する
```console
echo 'puts "merge!"' >> sample.rb
```
- コミットする
```console
git commit -m 'second commit'
```

- masterに移動
```console
git checkout master
```
- マージする
```console
git merge first_branch
```

- コミットが増えている
- --graphオプションをつけることでマージされ具合が分かりやすくなる
```console
git log --graph
```

