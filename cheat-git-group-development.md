
# cheat sheet [group development]

## 前提条件

ブランチは master, develop, feature/［featureブランチ名］の３段階で構成する

- master はマスターブランチ、基本的にリリースするファイルのみ
- develop は開発ブランチ、機能開発ブランチで作ったものをマージしていく
- feature/feature名 は機能開発ブランチ。機能ごとに作成し、機能開発が終わったら開発ブランチにマージし、機能開発ブランチは削除する

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

## フィーチャー毎の作業

### フィーチャー開発ブランチの立ち上げと切り替え

    $ cd <リポジトリディレクトリ名>
    $ git checkout -b develop
    ## ローカルのカレントブランチを「develop」にした

    $ git checkout -b feature/［featureブランチ名］
    ## ローカルカレントブランチ「develop」からフィーチャー開発ブランチ「feature/［featureブランチ名］」を作成する

    $ git branch -a
      develop
    * feature/feature-v0.3.0
      master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    ## 結果を確認
    ## 「feature/［featureブランチ名］」ブランチが作成され、カレントもそれになっている

    $ git checkout feature/［featureブランチ名］
    ## すでに存在しているフィーチャー開発ブランチ「feature/［featureブランチ名］」を取り出す場合は -b をつけない
    
    ##
    ## フィーチャー開発ブランチ上で開発する
    ##

### フィーチャー開発ブランチへのコミット
    
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
    $ git push origin feature/［featureブランチ名］
    ## リモート「feature/［featureブランチ名］」ブランチにpushする

### フィーチャー開発ブランチを開発ブランチへマージ

#### 単純にマージするだけの場合

    $ git checkout develop
    ## 開発ブランチ「develop」に切り替える

    $ git pull origin develop
    ## 最新の開発ブランチをリモートから取得する

    $ git merge feature/［featureブランチ名］
    ## フィーチャー開発ブランチを開発ブランチにマージする

    $ git push origin develop
    ## マージした内容をリモートの開発ブランチにプッシュする

#### プルリクエストを使う場合

- GitHubでリポジトリを開く。
- 「Pull requests」タブをクリック。
- 「New Pull Request」ボタンをクリック。
- 「base: develop」、「compare: feature/［featureブランチ名］」と設定。
- 変更内容を確認し、「Create Pull Request」をクリック。
- レビューが完了したら、「Merge Pull Request」をクリック。
- マージが完了したら、ローカルとリモートのフィーチャー開発ブランチを削除。

### フィーチャー開発ブランチの削除

    $ git branch -a
    ## ブランチの一覧を確認

    $ git branch -d feature/［featureブランチ名］
    ## ローカルフィーチャー開発ブランチを削除する
    
    $ git push origin --delete feature/［featureブランチ名］
    ## リモートフィーチャー開発ブランチを削除する
    ##  対象は origin、コマンドは --deleteオプション付きのpushで、パラメーターの feature/［featureブランチ名］ブランチを削除する意味になる

    
## 出典・参考
  コマンドで操作するgit - 開発手順に沿って解説
  https://qiita.com/ag3_product/items/d0312c90bff4c37bc5dc

