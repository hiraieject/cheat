
# cheat sheet [group development]

## 最初の作業

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
    
### フィーチャー開発ブランチの削除

    $ git branch -a
    ## ブランチの一覧を確認

    $ git branch -d feature/［featureブランチ名］
    ## 開発ブランチを削除する
    
    
## 出典・参考
  コマンドで操作するgit - 開発手順に沿って解説
  https://qiita.com/ag3_product/items/d0312c90bff4c37bc5dc
