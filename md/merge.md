### マージする
- ちょっと修正
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
```console
git log --graph
```

