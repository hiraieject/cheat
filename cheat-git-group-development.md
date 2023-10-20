
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

    $ cd <リポジトリディレクトリ名>
    $ git checkout -b develop
    ## ローカルのカレントブランチを「develop」にした

    $ git checkout -b feature/［featureブランチ名］
    ## ローカルカレントブランチ「develop」から開発ブランチ「feature/［featureブランチ名］」を作成する
    
    $ git branch -a
      develop
    * feature/feature-v0.3.0
      master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    ## 結果を確認
    ## 「feature/［featureブランチ名］」ブランチが作成され、カレントもそれになっている
    
    
    ## 開発する(ローカルでファイルを編集)
    
    $ git status
    $ git diff
    ## 開発ブランチの差分を確認する

    $ git add *
      or
    $ git add ［候補に加えたいファイル／ディレクトリ］
    ## 追加・変更したファイルをcommit候補に加える
    
## 出典・参考
  コマンドで操作するgit - 開発手順に沿って解説
  https://qiita.com/ag3_product/items/d0312c90bff4c37bc5dc
