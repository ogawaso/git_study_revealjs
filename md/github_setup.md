### githubアカウント作成
- githubのサイトに行く http://www.github.com
- 持ってない人はサインアップする

- SSH keysの作成する必要ある
- [設定方法](https://help.github.com/articles/generating-ssh-keys)を参考にしてください
```console
ssh-keygen -t rsa -C 'ogawaso@gmail.com'
```
```console
ls ~/.ssh/id_rsa.pub
```
- githubのサイトのメニューの右上のAccount Settingsのリンクを押す
- SSH keysを押す
- Add SSH keysリンクを押して公開鍵を貼付ける
- 確認方法
```console
ssh -T git@github.com
```
- 以下のような文言表示されたらOK
<pre>
Hi ogawaso! You've successfully authenticated, but GitHub does not provide shell access
</pre>

