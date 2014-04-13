#gitとは
- gitはソースコード管理システム
- ソースコード管理システムではこれまでVSS, cvs, subversionなどいろんなものがあった
- 1つのサーバー上に一括管理する集中管理じゃなくて分散管理
- 過去の履歴を変更できたり、かなり柔軟な操作が可能
- linuxを作ったlinusさんが最初に作って日本人がメンテナンスしている
http://itpro.nikkeibp.co.jp/article/COLUMN/20130418/471890/

# githubとは
- ソフトウェア開発プロジェクトのための共有ウェブサービス http://www.github.com
- 現在多くのオープンソースプロジェクトで採用
- gitを使っている
- GitHub Pageという機能があり、プロジェクト用のホームページを簡単に作ることができる
- https://pages.github.com/
- githubが世界中の人に使われることでgitが中心になっている

#今日の勉強会について
- gitをGUIを使わず、全てコンソール上でコマンドを使ってみる
- まずはコマンドに慣れる

#今日のあらすじ
- gitのリポジトリを作成
- githubアカウント作る
- githubにrepositoryを追加
- gitのコマンドを紹介
- githubを使ってpull-request(時間があれば)

# gitの中身の概要
- ファイルの変更を保存する場所をリポジトリという
- 自分の手元のPCのリポジトリをローカルリポジトリという
- 専用のサーバに配置しているリポジトリをリモートリポジトリという
- ファイルの追加、修正、変更などをコミットという操作でリポジトリに保存する
- リポジトリにコミットが時系列順に並ぶことで過去の変更履歴を参照できる
- ワーキングディレクトリー、インデックスと呼ばれる状態があり、様々なコマンドを叩くことで状態が変わる

# gitのインストール
osxには入っているはず
<pre>
$ git --version
</pre>

# gitの初期設定
## 設定済みの確認方法
<pre>
$ git config -l
</pre>

##何も設定してない方は
<pre>
$ git config --global --add user.name "ogawaso"
$ git config --global --add user.email ogawaso@gmail.com
</pre>

#オススメ設定1
##色付け
<pre>
$ git config --global color.ui auto
</pre>

##実は設定情報は以下のファイルに書かれている
<pre>
$ less ~/.gitconfig
</pre>

#リポジトリファイルを作成
- rubyファイルを例に
<pre>
$ mkdir git_study
$ cd git_study
$ echo 'puts "hello!"' > sample.rb
$ ruby sample.rb
$ git init 
</pre>

# 状態の確認
<pre>
$ git status
</pre>
<pre>
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)
  </pre>

# リポジトリ追加対象にする
<pre>
$ git add .
</pre>

## git add ファイル名
## git add -u
- 変更した複数のファイルを全て追加
## git add -p
- debugログを仕込んでいたときとか便利

# 追加対象になったことの確認
<pre>
$ git status
</pre>
<pre>
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

          new file:   sample.rb
          </pre>

#リポジトリへの追加
<pre>
$git commit -m 'first commit'
</pre>

# 履歴の確認
<pre>
$ git log
</pre>

## git log -p
実際の変更を表示

# tig
## git logをviのコマンドベースで見れる
## インストール法(osx)
- homebrewをインストール済み前提
<pre>
brew install tig
</pre>

# リモートリポジトリとしてgithubに保存する
- githubのサイトに行く http://www.github.com
- 持ってない人はサインアップする
## SSH keysの作成
<pre>
$ ssh-keygen -t rsa -C 'ogawaso@gmail.com'   ←自分のメールアドレスで
$ ls ~/.ssh/id_rsa.pub
</pre>
- githubのサイトのメニューの右上のAccount Settingsのリンクを押す
- SSH keysを押す
- Add SSH keysリンクを押して公開鍵を貼付ける

$ ssh -T git@github.com
Hi ogawaso! You've successfully authenticated, but GitHub does not provide shell access
</pre>

- githubのサイトで右上のプラスボタンを押す
- New Repositoryを選ぶ
- git_studyという名前でレポジトリの作成

# 送信先の追加の作成
$ git remote add origin git@github.com:ogawaso/git_study.git
$ git push -u origin master

- github上でリポジトリがあることを確認

#ブランチについて
- 履歴の流れを分岐できる
- 例として変更中の機能追加しているときに突発的なバグ改修をしたい時とかに使うと便利
-最初のコミットではmasterブランチが作られる
- masterがいつでもリリース可能な状態にする

# gitの操作
- ブランチにコミットしてマスターブランチにマージ
- すでにあるコミットを修正してみる


<pre>
$ git branch
$ git checkout -b first_branch
$ git branch # 2つあることを確認
</pre>


#ブランチへのコミット
<pre>
$ echo 'puts "hello! hello!"' >> sample.rb
$ git commit -m 'second commit'
</pre>
<pre>
$ git checkout master
$ git merge second
$ git log --graph
</pre>

#ファイルの削除
<pre>
$ git rm ファイル名
</pre>
#コメントを修正したい(最新のコミットを修正したい)
<pre>
$ git commit --amend
</pre>

#コミットするまではない編集を一時保存
<pre>
$ git stash
</pre>

## 一時保存したものを取得
<pre>
$ git stash pop
</pre>

## 一時保存した修正一覧
<pre>
$ git stash list 
</pre>

# コミットを元に戻す
<pre>
$ git revert [コミットID]
</pre>

#コミットを消す
## インデックスに戻す
<pre>
$ git reset --soft HEAD~1
</pre>

## 変更も消す
<pre>
$ git reset --hard HEAD~1
</pre>

#別のブランチの1つのコミットだけ持ってくる
<pre>
$ git cherry-pick コミットID
</pre>

#オススメ設定2
##エイリアス
<pre>
$ git config --global alias.co "checkout"
$ git config --global alias.ci "commit"
$ git config --global alias.au "add -u"
$ git config --global alias.br "branch"
</pre>


#pull-requestをやって見る
- ペアを組みましょう
- 片方がpull-requestを送る
- もう片方がpull-requestを受け取る

- 通常はfolkするけど、git_studyという名前があるからremote addする
<pre>
git remote add 対象者のアカウント git@github.com:対象者のアカウント/git_study.git 
git fetch
</pre>
## git fetchコマンド
- リモートからコミットを取得する

#リモートブランチを作る
<pre>
$ git checkout -b first-pull-request
$ echo 'puts "hello! pull-request!"' >> sample.rb
$ git push -u origin first-pull-request
</pre>

- github上でbranch一覧にブランチが追加されていることを確認
- ブランチを参照
- Create pull requestボタンを押す
- コメントを書く
- 作成ボタンを押す

#pull-requestを受け取る
- github上でpull-requests一覧を参照
- 詳細表示
- 問題ないかコメントのやり取り
- 承認ボタンを押す

# pull-requestをローカルで承認
- テストが動くことを確認
<pre>
$ git fetch
$ git checkout -b ブランチ名 リモート名/ブランチ名
</pre>

- テストとかしてみる
- 対象ブランチにマージ
<pre>
$ git pushする
</pre>


