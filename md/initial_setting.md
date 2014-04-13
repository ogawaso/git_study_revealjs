## gitの初期設定

- 設定済みの確認方法
```console
git config -l
```

- 何も設定してない方は
```console
git config --global --add user.name ogawaso
git config --global --add user.email ogawaso@gmail.com
```

- 色付け
```console
git config --global color.ui auto
```
- editor
```console
git config --global core.editor vim
```

- 設定情報が追加されてる
```console
git config -l
```
