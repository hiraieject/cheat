
# cheat sheet [git group development]

## 前提条件

ブランチは master, develop, feature/［機能開発ブランチ名］の３段階で構成する

- master はマスターブランチ、基本的にリリースするファイルのみ
- develop は開発ブランチ、機能開発ブランチで作ったものをマージしていく
- feature/【機能開発ブランチ名】は機能開発ブランチ。機能ごとに作成し、機能開発が終わったら開発ブランチにマージし、機能開発ブランチは削除する

## 最初の作業(開発ブランチの作成)

    $ git clone ［リポジトリパス］
    ## リモートリポジトリをローカルにクローンする

    $ cd <リポジトリディレクトリ名>
    $ git branch -a
    ## ブランチの一覧を確認

    $ git branch -a
    * master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    ## 最初はこうなっているはず
    
    $ git checkout -b develop
    Switched to a new branch 'develop'
    ## master から develop ブランチを作成

    $ git branch -a
    * develop
      master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    ## 結果を確認
    ## developブランチが作成され、カレントもdevelopブランチになっている

## 機能ブランチ毎の作業

### 機能開発ブランチの立ち上げと切り替え

    $ cd <リポジトリディレクトリ名>
    $ git status
    $ git checkout develop
    ## カレントブランチを確認し、「develop」でなければ「develop」に切り替え

    $ git checkout -b feature/［機能開発ブランチ名］
    ## ローカルカレントブランチ「develop」から機能開発ブランチ「feature/［機能開発ブランチ名］」を作成する

    $ git branch -a
      develop
    * feature/［機能開発ブランチ名］
      master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    ## 結果を確認
    ## 「feature/［機能開発ブランチ名］」ブランチが作成され、カレントもそれになっている

    $ git checkout feature/［機能開発ブランチ名］
    ## すでに存在している機能開発ブランチ「feature/［機能開発ブランチ名］」を取り出す場合は -b をつけない
    
    ##
    ## 機能開発ブランチ上で開発する
    ##

### 機能開発ブランチへのコミット
    
    $ git status
    $ git diff
    ## 開発ブランチの変更ファイル、差分を確認する

    $ git add *
      or
    $ git add ［候補に加えたいファイル／ディレクトリ］
    ## 追加・変更したファイルをcommit候補に加える
    
    $ git status
    ## 開発ブランチの状態を再度確認する
    
    $ git commit
      or
    $ git commit -m "［commitメッセージ］"
    追加・変更したファイルをcommitする
    
    $ git branch -a
    $ git push origin feature/［機能開発ブランチ名］
    ## リモート「feature/［機能開発ブランチ名］」ブランチにpushする

### 機能開発ブランチを開発ブランチへマージ

#### 単純にマージするだけの場合

    $ git checkout develop
    ## 開発ブランチ「develop」に切り替える

    $ git pull origin develop
    ## 最新の開発ブランチをリモートから取得する

    $ git merge feature/［機能開発ブランチ名］
    ## 機能開発ブランチを開発ブランチにマージする

    $ git push origin develop
    ## マージした内容をリモートの開発ブランチにプッシュする

#### プルリクエストを使う場合

最新のdevelopブランチを取り込む

    $ git checkout feature/[機能開発ブランチ名]
    $ git pull origin develop

GitHubでリポジトリを開く。

「Pull requests」タブをクリック。

「New Pull Request」ボタンをクリック。

「base: develop」、「compare: feature/［機能開発ブランチ名］」と設定。

変更内容を確認し、「Create Pull Request」をクリック。

「Pull requests」を受けて、レビュアーがレビューを実施

レビューが完了したら、「Merge Pull Request」をクリック。

マージが完了したら、ローカルとリモートの機能開発ブランチを削除。

最新のdevelopブランチをローカルに取り込む

    $ cd <リポジトリディレクトリ名>
    $ git status
    $ git checkout develop
    ## カレントブランチを確認し、「develop」でなければ「develop」に切り替え
    
    $ git pull origin develop
    ## 最新の開発ブランチをリモートから取得する

別の機能ブランチを別フォルダで開発している場合は、developブランチにマージされた内容を取り込む

    $ git checkout feature/[機能開発ブランチ名]
    ## カレントブランチを機能ブランチに切り替える

    $ git merge develop
    ## 最新の開発ブランチを機能ブランチにマージする

    ここまででローカルのリポジトリのみにマージ内容が反映された状態になる
    リモートにも反映する場合は以下を実行
    
    $ git add .
    $ git commit -m "developブランチから最新の変更をマージ"
    $ git push origin feature/[機能開発ブランチ名]
    ## ローカルリポジトリにマージした developブランチのマージ内容を、リモートリポジトリに反映

### 機能開発ブランチの削除

    $ cd <リポジトリディレクトリ名>
    $ git status
    $ git checkout develop
    ## カレントブランチを確認し、「develop」でなければ「develop」に切り替え

    $ git branch -a
    ## ブランチの一覧を確認

    $ git branch -d feature/［機能開発ブランチ名］
    ## ローカル機能開発ブランチを削除する
    
    $ git push origin --delete feature/［機能開発ブランチ名］
    ## リモート機能開発ブランチを削除する
    ##  対象は origin、コマンドは --deleteオプション付きのpushで、パラメーターの feature/［機能開発ブランチ名］ブランチを削除する意味になる

    
## 出典・参考
  コマンドで操作するgit - 開発手順に沿って解説
  https://qiita.com/ag3_product/items/d0312c90bff4c37bc5dc

